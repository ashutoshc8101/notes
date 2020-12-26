#### Notes

# Angular

### 1. Lifecycle events:
- ngOnChanges() -> Respond when Angular sets or resets data bound input properties
                -> Called before ngOnInit() and when data-bound input properties change

- ngOnInit()    -> Intialize the component after Angular first displays data-bound properties
                -> Called once, after the first ngOnChanges()
 
- ngDoCheck() -> Detech and act upon changes that Angular won't detect on it's own
              -> Called immediately after ngOnChanges() on every detection run after                         -> ngOnInit()  on first run
              
- ngAfterContentInit() -> Respond after Angular projects external content into view
               -> Called after ngAfterContentInit() and every subsequest ngDoCheck()  
               
- ngAfterContentChecked() -> Respond after Angular checks content project into the component                   -> Called after ngAfterContentInit() and every subsequent ngDoCheck()

- ngAfterViewInit() -> Respond after Angular initializes the component's viws and child views,
                    -> Called once after the first ngAfterContentChecked()
                 
- ngOnDestroy() -> Cleanup just before Angular destroys the directive or component.
                -> Called immeditately before Angular destroys the component
 
##### Important Points
* Components should be cheap and safe to construct. You should not, for example, fetch data in a component constructor. An ngOnInit() is a good place for a component to fetch its initial data.
* Constructors should do no more than set the initial local variables to simple values.
* Keep in mind that a directive's data-bound input properties are not set until after construction. If you need to initialize the directive based on those properties, set them when ngOnInit() runs.

* Put cleanup logic in `ngOnDestroy()`, 
  - This is place to free resources that won't be garbage-collected automatically.
      * Unsubscribe from Observables and DOM events.
      * Stop interval timers.
      * Unregister all callbacks that the directive resgistered with global or application `         services.
      
### 2. View encapsulation   
   Component css styles are encapsulated into the component's view and don't affect the rest of the application.
   To control how encapsulation happens, you can set the view encapsulation mode in the component metadata.
   - `ShadowDom` view encapsulation uses the browser's native shadow DOM implementation
   - `Emulated (default)` emulates the behavior of shadow DOM by preprocessing the CSS code.
   - `None` means Angular won't do view encapsulation. Angular adds CSS to gloabl styles.
 
### 3. Templates
To emlimite the risk of script injection, Angular doesnot support <script> elements within templates.
    - Text interpolation using {{ }} can be used in urls and can also invoke functions

With interpolation, Angular performs the following tasks:

  1. Evaluates all expressions in double curly braces.
  2. Converts the expression results to strings.
  3. Links the results to any adjacent literal strings.
  4. Assigns the composite to an element or directive property.

You can use all javascript expressions in interpolation syntax except these:
  * Assignments (=, +=, ...)
  * Operators such as `new`, `typeof`, or `instanceof`
  * Chaing expressions with `;` or `,`
  * The increment and decrement operators `++` and `--`
  * some of the ES2015+ operators
 
Other notable differences from Javascript syntax include:
  * No support for the bitwise operators such as | and &
  * New template experession operators such as |, ? and !
  
Expression context:
  Expression context is the union of template variables, the directive's context object and   component's members.
  
Expression best practices
When using template expressions, follow these best practices:
  * Use short expressions
  * No visible side effects. -> a template expression should not change any application        state.
  
##### Idempotent expression:
   Idempotent expression is free of side effects and improves Angular's change detection        performance. An idempotent expression always returns exactly the same thing until one of its dependent values changes.
   
### 4. Template statements
  Template statements are methods that you can use in your HTML to respond to user events.
  template statement syntax `(event)="statement"` eg -> `(click)="handleClick($event)"`
  
  Template statements additionally supprots both basic assignment, =, and chaining expressions with semicolons,:
  
##### Statement best practices
- Conciseness
- Keep template statements minimal by using method calls or basic property assignments.
- Work within the context

  The context of a template statement can be the component class instance or the template.     Because of this, template statements cannot refer to anything in the global namespace such   as window or document. For example, template statements can't call console.log() or     Math.max().
  
  
