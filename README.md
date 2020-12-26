#### Notes

# Angular

#### Lifecycle events:
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
 
### Important Points
* Components should be cheap and safe to construct. You should not, for example, fetch data in a component constructor. An ngOnInit() is a good place for a component to fetch its initial data.
* Constructors should do no more than set the initial local variables to simple values.
* Keep in mind that a directive's data-bound input properties are not set until after construction. If you need to initialize the directive based on those properties, set them when ngOnInit() runs.

* Put cleanup logic in `ngOnDestroy()`, 
  - This is place to free resources that won't be garbage-collected automatically.
      * Unsubscribe from Observables and DOM events.
      * Stop interval timers.
      * Unregister all callbacks that the directive resgistered with global or application `         services.
      
### View encapsulation   
   Component css styles are encapsulated into the component's view and don't affect the rest of the application.
   To control how encapsulation happens, you can set the view encapsulation mode in the component metadata.
   - `ShadowDom` view encapsulation uses the browser's native shadow DOM implementation
   - `Emulated (default)` emulates the behavior of shadow DOM by preprocessing the CSS code.
   - `None` means Angular won't do view encapsulation. Angular adds CSS to gloabl styles.
 
### Templates
To emlimite the risk of script injection, Angular doesnot support <script> elements within templates.
    - Text interpolation
