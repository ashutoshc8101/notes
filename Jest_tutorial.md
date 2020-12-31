## Expect

When you're writing tests, you often need to check that values meet certain conditions. `expect` gives you access to a number of "matchers" that let you validate different things.

```javascript
// Matchers

test(' 2 + 3 equals 5 ', ()=> {
    expect(2+3).toBe(5)
})

test('object assignment', ()=>{

    const data = {one: 1}
    data['two'] = 2;
    expect(data).toEqual({one: 1, two: 2})

})

test('array assignment', ()=>{
    const ar = [1,2,3,4,5]
    expect(ar).toEqual([1,2,3,4,5])
})

it('is null', ()=>{
    expect(null).toBeNull()
})

it('is undefined', ()=>{
    expect(undefined).toBeUndefined()
})

it('is defined',()=>{
    expect(2).toBeDefined()
} )

it('is truthy', ()=>{
    expect(1=='1').toBeTruthy()
})

it('is falsy', ()=>{
    expect(0).toBeFalsy()
})

it('two plus two', ()=>{
    let value = 2 + 2
    expect(value).toBeGreaterThan(3)
    expect(value).toBeGreaterThanOrEqual(4)
    expect(value).toBeLessThan(5)
    expect(value).toBeLessThanOrEqual(4)

    expect(value).toBe(4)
    expect(value).toEqual(4)
})

it('checks floating point numbers', ()=>{
    const value = 0.2 + 0.1;

    expect(value).toBeCloseTo(0.3)
})

it('there is no I in team', ()=>{
    expect('Team').not.toMatch(/I/)
})

test('there is a stoph in Christoph', ()=>{
    expect('Christoph').toMatch(/stoph/)
})

test('the shopping list has milk on it', ()=>{
    expect(['milk', 'apples']).toContain('apples')
    expect(new Set(['milk', 'apples'])).toContain('milk')
})


test('compling goes as expected', () => {
    function compile() {
        throw new Error('Erroring')
    }
    expect(()=> compile()).toThrow('Error');
}) 


// Matchers ends

```

## Asynchronous testing.

```javascript

// AJAX testing with callback
function fetchDataWithCallback(clb) {

    setTimeout(() => {
        clb([1,2,3])
    }, 1000)


}

test('async code with callback', (done)=>{

    fetchDataWithCallback((data) => {
        try{
            expect(data).toContain(2);
            done()
        } catch(error) {
            done(error)
        }
    })
})

// AJAX testing with Promises

function fetchDataWithPromise(fail = 0) {

    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if(fail) {
                reject('Failed')
            }else{
                resolve([1,2,3])
            }
        })
    })
}

test('async code with promises', ()=>{

    expect.assertions(1)
    return fetchDataWithPromise(1).then((data)=>{
        expect(data).toContain(1)
    }).catch(e => expect(e).toMatch('Failed'))
})

test('async code with promises with resolves and rejects', () => {

    return expect(fetchDataWithPromise()).resolves.toEqual([1,2,3])
})

test('async code with promises rejects', ()=>{

    return expect(fetchDataWithPromise(1)).rejects.toMatch('Failed')
})

test('async code with promises with async/await', async () => {

    expect.assertions(1)
    try{
        await fetchDataWithPromise(1)
    } catch (e) {
        expect(e).toMatch('Failed')
    }
})

// Best methods
test('async code with async await', async () => {

    await expect(fetchDataWithPromise()).resolves.toEqual([1,2,3])
})

test('async code rejects with async await', async () => {

    await expect(fetchDataWithPromise(1)).rejects.toMatch('Failed')
})

```
