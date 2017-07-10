# Angular Course notes

## SECTION 1: INTRODUCTION

* Angular creates one page web apps. As the users browses the app, content is dynamically loaded into the html using Javascript. (Without changing url)
* Angular 2 is completely different than angular 1. Angular 4 is an update to Angular 2 (or just 'Angular')
* src folder is where the work happens. Assets folder can be used to store static files like images etc, app folder is for the app code. and the environments folder can be used to store needed variables
* In Angular we use components to build up the page
* with [(ngModel)]="" you can bind something to a property of the component.ts, which is connected to the html file. the .html is what you see, while the .ts is the logic behind it
* Directives are helpers/instructions you can place in your html template which will do something at runtime depending on what commands you gave it
* Typescript is a Javascript superset. It offers more features than Javascript like classes, interfaces, types. Uses strong typing(you define if something is a string, number etc). Builds into vanilla JS
* Angular-cli.json allows you to define imports of global stylesheets

## SECTION 2: The Basics

* The server serves the index.html file to the browser
* In the component.ts the decorator has a selector which gives it a name, for example 'app-root'. This can than be used in the index.html like <app-root></app-root> to connect it with that component. Component.html has the actual content
* When using ng serve to save your project, it bundles the needed Javascript files and adds them to the html (files Angular needs to work)
* main.ts is the code that gets exectured first on page load
* platformBrowserDynamic().bootstrapModule(AppModule); starts/bootstrapts the Angular app by passing a 'AppModule' to this method. And 'AppModule' refers to the app.module.ts file
* main.ts starts things off by bootstrapping an angular app, passes AppModule as an argument -> in this module you say that there is a app.component which should be known when you start yourself(bootstrap array) -> Angular checks the component.ts and now knows the selector (eg: <app-root>) and now is able to handle this selector in the index.html file

### COMPONENTS

* Your app is build by composing multiple components (You start off with the app/root component, which holds the entire app by nesting components within it)
* Angular components allow you to split up a big app in multiple reusable parts. Each component with it's own 'busines logic'/styling
* New components you create aren't added to the bootstrap array, thus directly to the index.html. But instead are added to the app.component.html. As this is the root component (because it's called on by main.ts and added in the bootstrap array in the app.module.ts)
* Generally all your app related subfolders and files go into the 'app' folder. This includes new components
* It's good practice that each component has it's own folder
* It's good practice to name a component like this: name.component.ts
* A component is a typescript class. Angular uses this as a blueprint to create objects with it
* Using export class makes it so that a component can be used outside of it's own file, like in other components
* Typescript decorators can be used to 'enhance' your classes and other elements of code
* Using import { Component } from '@angular/core'; you can important the decorator @Component so angular knows to use it. Within @Component you can store metadata about the class
* 'Selector' within a class decorator is basically the HTML tag which you can use to call this component in templates (has to be unique)
* 'templateUrl' let's you define the html template file that the specific component uses
* Modules are used to bundle up multiple components into 'packages', describing which functionalities and features these components use
* Modules start off as a component but are transformed into something else by using a decorator. the @NgModule decorator
* New components need to be registered in the module so Angular knows it's there. Angular won't scan all your files automatically
* @NgModuyle has declarations. This is where you can declare new components to be used
* Added components need to be imported into the module
* 'imports' in @NgModule let's you import other modules into this one. To make this one a bit leaner and outsource some stuff
* You can create components using the cli with 'ng generate component name'. This creates the folder structure within the app folder with the component files
* You can nest components by calling their selector in a html template, and then calling the component to which that html belongs again in another component
* Each component has to have a template or a templateUrl defined. Depending if you want a seperate template or inline templateUrl. Styles and selectors are optional, but template/templateUI isn't
* Styles can be defined inline or externally by using styleUrls. StyleUrls is an array so you can use multiple external stylesheets
* using styles inline within the component.ts is done by creating an array of objects, with properties as style lines
* You can use the component selectors in multiple ways. You can use a html tag, class or attribute as the selector name to call it within the html template
* The constructor in the export class is a method that's executed at the moment that the component is created by Angular(method typescript has which is called once component is created)

### DATABINDING

* Databinding is a communication between your component Typescript code and the html template (output data or react to user events)
* String interpolation {{ data }}
* Property binding [property]="data"
* Event binding (event)="express", this allows to react to user input, like clicking a link
* Two-way-databinding (reacting to user events and outputting data at the same time)

#### String interpolation (outputting data in a template)

* Using {{VARIABLE}} you can have a piece of data that's exported by the component in the html, instead of a static string
* You put methods or strings between the {{}}, whatever is between it; it must return a string in the end (no multiline expressions like IF)

#### Property binding

* `[disabled]="!allowNewServer"` allows you to bind a property to a html element. This can be a method which returns true/false
* Binding the elements (native) property to our typescript property, if our property in the typescript file changes, this is updated automatically in the DOM
* This is a power of Angular, it enables you to easily interact with your DOM and change things in runtime
* You can bind to html elements, directives and your own components.

#### Property binding VS string interpolation

* Instead of string interpolation {{STRING}} you can databind a string to the element like `[innerText="STRING"]`
* If you want to put some text into your html use string interpolation, if you want to dynamically change a property use property binding
* Don't mix property binding and string interpolation

#### Event binding

* Events use () instead of [] to signal event binding `(click)="METHOD()">`
* As a general rule you don't want to put too much logic into your template, but instead in your typescript and use methods to call it
* You can bind to all properties and events, use console.log() on the elements to see which properties and events it offers
* For events you don't bind to onclick but only to click (=> (click))
* Google YOUR_ELEMENTS properties or YOUR_ELEMENT events to see lists
* `$event` is a variable used to send the data to the method. An event has data, like click location or input value. With `$event` we can capture this data and use it
* (<HTMLInputElement>event.target).value; This tells Typescript that we're getting the value from an HTML element


#### Two-way binding

* Instead of (input) you can use `[(ngModel)]="serverName"`. This is called using a directive. It will trigger on input event and update the variable automatically
* Using two-way binding, the ngModel updates the value of the input aswell as the variable it refers too in the method.
* Two-way binding is an easy way to react to an event in both directions
* In order for two-way binding to work you need to enable the ngModel directive. This is done by adding FormsModule to the imports[] array in the AppModule
* You also need to important the `@angular/forms` in the app.module.ts file `import { FormsModule } from '@angular/forms';`

### Directives

* Directives are instructions in the DOM. For example using a component selector in the HTML to tell angular to use it. Components are directives with templates
* `<p appTurnGreen>Receives a green background!</p>` is a directive without a template. It's a custom directive which instructs Angular to do something in the DOM
* Directes are used with the attribute selector (css classes are also possible just like with component selectors)
* Using the `@Directive({})` decorator you can define the selector, you can write the logic for it in the TS file

#### build in Angular directives

##### ngIf (structural directive)

* ngIf directive allows you to conditionally output data
* Use a `*` symbol (#ngIf) before a directive when it changes something in the structure of the DOM. Either adding or removing elements
* #ngIf requires a true/false. `#nfIg="true/false"` or an expression that returns true or false
* nfIf adds or removes elements from the DOM, it doesn't just hide them
* if looping through an array with ngIf, the ngIf needs to be in the ngFor, meaning in a child element etc
* Using a marker you can set an else for the ngIf:

```
<p *ngIf="serverCreated; else noServer">Server was created, server name is {{serverName}}</p>
<ng-template #noServer>
    <p>
        No server was created
    </p>
</ng-template>
```

##### ngStyle (attribute directive)

* attribute directives don't add or remove elements in the DOM. They only change the element they were placed on
* Using [ngStyle], the square brackets aren't part of the directive name. We only indicate that we want to bind the directive to a property
* `[ngStyle]="{backgroundColor: getColor()}">` we're binding a method which returns a color to the element:
```
getColor() {
    return this.serverStatus === 'online' ? 'green' : 'red';
}
````
* ngStyle allows us to dynamically update styles

##### ngClass

* ngClass allows you to enter classes conditionally (true/false)
* [ngClass]="{online: serverStatus === 'online'}", the online class is added to the element if the server is online

##### ngFor (structural directive)

* loop through an array and create elements based on it ( for of loop)
* `<app-server *ngFor="let server of servers"></app-server>`, this loops through server and assign a <app-server> component for each in the array
* `*ngFor="let logItem of log; let i = index"` this gives you access to the index of the current iteration, when looping an array

## SECTION 3: Course project - The Basics

* in .angular-cli.json you can define which files are bundled, css etc
*` ng generate(g) component(c) --spec false` let's your create a component folder through the cli
* (TYPESCRIPT) A model is a typescript file which holds a model of an object, a blueprint for an object we create
* (TYPESCRIPT) `public name: string;` this let's the export class know that the property can be accessed by anyone, the string indicates what type of value it holds
* (TYPESCRIPT) a constructor is a build in function each class has that initializes upon creating the class
* `[src]="recipe.imagePath"` and `src="{{recipe.imagePath}}"` would both work, one is property binding and one is string interpolation
* You can use make a TS model using a shortcut like so;
```
export class Ingredient {
    constructor(public name: string, public amount: number) {}
}
```

## SECTION 4: Debugging

### Console

* If an error occurs when you try to fire an event, the bug is probably in a method that you're trying to call at that moment
* If something is undefined you have to set a property to something. doing `servers;` doesn't let it know what it is. Use `servers = [];` instead

### Debugging in browser using Sourcemaps

* Sourcemaps allow the browser to change JS code to typescript, or map the javascript to our Typescript files
* Open Sourcemaps by clicking on the line number in the javascript file in sources
* In sources and in the webpack folder, then the . folder, you can find all your typescript files for debugging

### Angular Augury

* Augury allows you to dive into your Angular application and see the components etc.

## SECTION 5: Components & Databinding Deep Dive

* With property binding we pass information to the element, for example letting it know if disabled should be true or false
* Same with event binding, we emit an event to our Typescript code with input data etc
* We can use property and event binding on HTML elements, but also on directives and components (to send information between components, emitting our own events)

### Custom property binding

* Custom property binding allows you to emit events between components, sending information/data between them
* By default all properties inside components are only accessible inside the components `@Input()` before a property let's it be accessed by parent components
* When @Input() is used any parent component of other components are able to access the property
* You can use a custom property name like so `@Input('srvElement')`

### Custom event binding

* `(serverCreated)="onServerAdded($event)"` This is a custom event
* `@Output() serverCreated = new EventEmitter<{serverName: string, serverContent: string}>();` let's you define a custom event in your Typescript file
* `@Output()` needs to be defined before the EventEmitter

### View Encapsulation

* CSS styles will only get applied to the component they belong too, this is view encapsulation (behavior enforced by Angular, not browsers)
* Angular gives all elements in a component a certain attribute so the style is only applied to it, for example; `_ngcontent-ejo-1`
* With `encapsulation: ViewEncapsulation.None` in your @component decorator you can define if a component uses view encapsulation
* Emulated: encapsulated, none: global, native: shadow-dom when supported

### Local references in templates

* A local reference can be placed on every HTML element
* You can use local references only in the specific template(not in the TS file)
* `#serverNameInput` this is how you define a local reference
* `(click)="onAddServer(serverNameInput)"` passing a local reference to your TS file like with a click event
* So a local reference can be used within template or passed on to your TS code
* @ViewChild (needs to be imported from @angular/core) let's you call a local reference in your TS file
* @ViewChild returns ElementRef, this is a element reference
* So you can send a local reference through a method parameter in your template, or fetch it through @ViewChild `  @ViewChild('nameInput') nameInputRef: ElementRef;`

### ng-content (passing data)

* Everything you place between the opening and closing tag of your own component selector, is removed by Angular
* `<ng-content></ng-content>` If this is placed in a component, anything you place between the opening and closing tag of that component will be placed where <ng-content> is within it
* This is if you have a reused piece of functionality that you don't want to pass through data binding

### Component lifecycle hooks (ngOnInit)

* When Angular comes across a selector for a component it will initiate it, and it will go through several phases. We can a chance to hook into these phases to execute some code
* If certain methods are present Angular will execute them:

#### Hook 1: ngOnChanges

* ngOnChanges is called right at the start when the component is created, and whenever one of our bound input properties (@input) changes
* `ngOnChanges(changes: SimpleChanges) {`, ngOnChanges requires this argument

#### Hook 2: ngOnInit

* ngOnInit gets called when Angular finishes the basic initialization of the component, this doesn't mean the component is in the HTML yet, but the object was created
* ngOnInit will run after the constructor

#### Hook 3: ngDoCheck

* ngDoCheck runs whenever change detection runs. Change detection is when Angular sees that something needs to be changed in the HTML template
* Even if nothing changes in the HTML, if you fire an event or something that could cause a change, ngDoCheck will run
* ngDoCheck has a lot of different triggers, events, data changes etc

#### Hook 4: ngAfterContentInit

* ngAfterContentInit is called after the content that is projected via ng-content has been initialized
* Not the view of the component itself, but the view of the parent component and specifically the part inside the <selectors>

#### Hook 5: ngAfterContentChecked

* ngAfterContentChecked will be called whenever the ng-content is checked

#### Hook 6: ngAfterViewInit

* ngAfterViewInit will be initialized once the view of the component has been rendered
* AfterViewInit gives you access to the template elements, before this hook has been reached you can't do that

#### Hook 7: ngAfterViewChecked

* ngAfterViewChecked will be called every time the view have been checked

#### Hook 8: ngOnDestroy

* ngOnDestroy is called when a component is about to be destroyed, right before it
* good to use for some clean up work

### @ContentChild

* ContentChild let's you access what's inside a ng-content, by selecting the parent element using ElementRef `@ContentChild('contentParagraph') paragraph: ElementRef;`

## Section 6: Components & Databinding

* `@Input()` can be used to get data from a parent component to a child component:
```
<app-recipe-item
    *ngFor="let recipeEl of recipes"
    [recipe]="recipeEl"></app-recipe-item>
```
the child component (recipe-item) will receive the [recipe] data. In it's TS you need to @Input() the recipe from it's parent to receive `import { Recipe } from '../recipe.model'`

## Section 7: Directives Deep Dive

* Attribute directives sit on elements just like attributes
* Structural directives do the same, but they also change the structure around the element. It can remove elements from the DOM altogether

### Attribute directives

* Look like a normal HTML Attribute, possibly with databinding or event binding
* Only affect/change the element they are added to

### Structural Directives

* Look like a normal HTML Attribute but havbe a leading *
* Affect a whole area in the DOM, elements get added/removed

### ngFor / ngIf

* When looping with ngFor, you can use the item on any element that's nested within the element that has ngFor
* You can only have one structural attribute per element
* `*ngIf="onlyOdd"` onlyOdd returns true/false, with this you can filter elements based on data

### ngClass / ngStyle

* `[ngClass]="{odd: odd % 2 !== 0}"` Here you assign the class odd to the element if the number is odd
* `[ngStyle]="{backgroundColor: odd % 2 !== 0 ? 'yellow' : 'transparent'}"` here you give the element a background color of yellow if the number is odd, otherwise transparent

### Creating a custom Directive

* Defing a directive;
```
import { Directive } from '@angular/core';

@Directive({
    selector: '[appBasicHighlight]'
})

export class BasicHighlightDirective {
    constructor() {}
}
```
* If you now add appBasicHighlight to an element the directive will be recognized
* A Directive doesn't have a view/template
* This directive changes the element background to green:
```
import { Directive, ElementRef, OnInit } from '@angular/core';

@Directive({
    selector: '[appBasicHighlight]'
})

export class BasicHighlightDirective implements OnInit {
    constructor(private elementRef: ElementRef) {
    }

    ngOnInit() {
        this.elementRef.nativeElement.style.backgroundColor = 'green';
    }
}
```
* Directives need to be declared in the module.ts just like components to be used
* It's not a good practise to directly access your elements using ElementRef, use the Renderer helper

#### Renderer helper [Renderer docs](https://angular.io/api/core/Renderer2)

* This is a directive using the Renderer to manipulate the element:
```
import { Directive, Renderer2, OnInit, ElementRef } from '@angular/core';

@Directive({
  selector: '[appBetterHighlight]'
})
export class BetterHighlightDirective implements OnInit {

  constructor(private elRef: ElementRef, private renderer: Renderer2) { }

  ngOnInit() {
      this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'green');
  }
}
```
* Renderer is a better approach because Angular sometimes works outside of the browser without having the DOM, like with service workers
* [Renderer docs](https://angular.io/api/core/Renderer2)

#### @HostListener

* Needs to be imported from @angular/core
* This let's you listen to events from the Element
* Convenient way of listening to events, can be used with custom events
```
@HostListener('mouseenter') mouseover(eventData: Event) {
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'orange');
}

@HostListener('mouseleave') mouseleave(eventData: Event) {
    this.renderer.setStyle(this.elRef.nativeElement, 'background-color', 'transparent');
}
```

#### @HostBinding

* With @HostBinding you can define to which property(eg: style) of the host element(the element that carries the directive) you want to bind
* `@HostBinding('style.backgroundColor') backgroundColor: string = 'transparent';`, Here we're asking Angular to access the style(bg color) of the element that has the directive, and we set it equal to the background color defined

#### Binding to directive properties

* You can use custom property/event binding in directives
* Example of a custom property bind:
```
export class BetterHighlightDirective implements OnInit {
  @Input() defaultColor: string = 'transparent';
  @Input('appBetterHighlight') highlightColor: string = 'orange';
  @HostBinding('style.backgroundColor') backgroundColor: string;

  constructor(private elRef: ElementRef, private renderer: Renderer2) { }

  ngOnInit() {
      this.backgroundColor = this.defaultColor;
  }

   @HostListener('mouseenter') mouseover(eventData: Event) {
       this.backgroundColor = this.highlightColor
   }

   @HostListener('mouseleave') mouseleave(eventData: Event) {
       this.backgroundColor = this.defaultColor
   }

}
```
```
<p [appBetterHighlight]="'purple'" [defaultColor]="'yellow'">
    Style with me with better directive;
</p>
```
* You can bind a property without quotation marks `defaultColor="yellow"` instead of `[defaultColor]="'yellow'"` if it's a string and you remove the single quotation marks too

#### Structural directive: behind the scenes

* The star `*ngFor` let's angular know that it is a structural Directive
* `<ng-template>` isn't rendered, but it's a template that Angular can render if it needs to be rendered
* Angular transformers the `*` star to a regular property bind in a ng-template, the star is because it makes the syntax easier
* So `*ngIf='kek'` = `<ng-template [ngIf]="kek"</ng-template>`

#### Building a structural Directive

* `@Input() set unless(condition: boolean) {}` with set we can call a method, it's still a property but it sets a method which gets executed whenever the property changes
* `constructor(private templateRef: templateRef<any>) { }` This lets you inject a reference to the <ng-template>
* `constructor(private templateRef: TemplateRef<any>, private vcRef: ViewContainerRef) { }` ViewContainerRef marks the place where you placed this directive in the document
* This is a stuctural directive that either adds or removes something from the DOM:
```
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[appUnless]'
})
export class UnlessDirective {
  @Input() set appUnless(condition: boolean) {
    if (!condition) {
        this.vcRef.createEmbeddedView(this.templateRef);
    } else {
        this.vcRef.clear();
    }
  }

  constructor(private templateRef: TemplateRef<any>, private vcRef: ViewContainerRef) { }

}
```
binding in HTML:
```
<div *appUnless="method">
```

#### ngSwitch

* ngSwitch let's you show something if a certain value switches
* Handy if you need a lot of ngIf, maybe ngSwitch is a better solution in such cases
```
<div [ngSwitch]="value">
    <p *ngSwitchCase="5">Value is 5</p>
    <p *ngSwitchCase="10">Value is 10</p>
    <p *ngSwitchCase="100">Value is 100</p>
    <p *ngSwitchDefault>Value is Default</p>
</div>
```

## Section 8: Project Directives

A directive that toggles class on click:
.ts file
```
import { Directive, HostListener, HostBinding } from '@angular/core';

@Directive({
    selector: '[appDropdown]'
})

export class DropdownDirective {
    @HostBinding('class.open') isOpen = false;

    @HostListener('click') toggleOpen() {
        this.isOpen = !this.isOpen;
    }
}
```
.html file
```
<li class="dropdown" appDropdown>
```

## Section 9: Services & Dependency Injection

### Services

* Duplication of code and data storage are use cases for a Service
* A service is a class/piece in your Angular app which serves as kind of a repository for your code. Something where you can store/centralize your code in
* Services can be helpful in communicating between components

### Dependency Injector / Injecting Services

* A dependency is something our classes will depend on. For example a new account component depends on the login service because you want to call a method in that service
* The dependency injector injects an instance of this class into the component automatically, we need to inform Angular that we require the instance
* this is how you inject a service dependency. Use the class name as type. While constructing the component Angular will inject the service:
```
import { LoggingService } from '../logging.service';
```
```
providers: [LoggingService]
```
```
constructor(private LoggingService: LoggingService) {}
```
* Providors tells Angular how to provide the Service we need
* Calling/using the Service after it's been injected: `this.LoggingService.logStatusChange(accountStatus);`
* In bigger apps where you duplicate code a Service can help to lean down your script, you can simply outsource your code into a service and have it injected into components

#### Data service

```
export class AccountsService {
    accounts = [
      {
        name: 'Master Account',
        status: 'active'
      },
      {
        name: 'Testaccount',
        status: 'inactive'
      },
      {
        name: 'Hidden Account',
        status: 'unknown'
      }
    ];

    addAccount(name: string, status: string) {
        this.accounts.push({name: name, status: status});
    }

    updateStatus(id: number, status:string) {
        this.accounts[id].status = status;
    }
}
```

#### Hierarchical Injector

* the Angular dependency injector is a hierachrical injector, this means that if we provide a service in our app, eg: in a component, the Angular framework knows how to create a service for the component and all it's child components
* The component that has the service injected, as well as all the child components, will receive the same instance of the service
* If you provide a service in the app module, the same instance of that service is available in the entire app. In every component, directives etc
* If you provide the same service in a child component, the origin instance of the parent service gets overridden
* To avoid this simply remove the service from the providors array in the child components, the rest stays the same (import/constructor)

#### Injecting services into services

* Putting a service into the app.module gives the entire app the same instance of that service, this allows injecting a service into another service
* Injecting a service into another service:
```
constructor(private loggingService: LoggingService) {

}
```
Injecting needs metadata, so you can add `@Injectable()` (which needs to be imported from @angular/core) in the service that receives the other service
* `@Injectable()` is added on the service where you want to inject something, this tells angular that it's possible
* The injected service (in another service) still needs to be provided in the app.module

#### Using services for cross-communication between components

* You don't use to use input/output to communicatie between components with services
* Add the event emitter `statusUpdated = new EventEmitter<string>();` in the service, this can then be called by all components which have the service injected `this.accountService.statusUpdated.emit(status);`

## Section 10: Services & Dependency injection in project

* Example of a service with a private array and a method that exports it:
```
import { Recipe } from './recipe.model';

export class RecipeService {
    private recipes: Recipe[] = [
        new Recipe('A Test Recipe kek', 'This is simply a test kek', 'http://jetspizza.com/dbphotos/display/c161462910486f60cf38484ecf458adf/664/410'),
        new Recipe('A Test Recipe', 'This is simply a test kek lelzi', 'http://jetspizza.com/dbphotos/display/c161462910486f60cf38484ecf458adf/664/410')
    ];

    getRecipes() {
        return this.recipes.slice();
    }
}
```
* Subscribing to a service change:
```
ngOnInit() {
    this.ingredients = this.slService.getIngredients();
    this.slService.ingredientsChanged
        .subscribe(
            (ingredients: Ingredient[]) => {
                this.ingredients = ingredients;
            }
        )
}
```

## Section 11: Routing/router/routes

* Routing implies navigating by url dash without actually loading a new page, aka changing views
* Routes are app-wide, so it's a good idea to set them in the app.module.ts
* `import { Routes, RouterModule } from '@angular/router';` needs to be imported
* Also add RouterModule to the imports array `RouterModule.forRoot(appRoutes)` forRoot lets Angular know what const you're using for your routes and to use them
* Routing setup:
```
const appRoutes: Routes = [
    { path: '', component: HomeComponent }, //localhost:4200/users
    { path: 'users', component: UsersComponent },
    { path: 'servers', component: ServersComponent }
];
```
### RouterLink

* `<router-outlet></router-outlet>` in your HTML marks the place where Angular will place the component linked to the route
* Adding regular `href="/users"` links reloads the app, use `routerLink="/"` instead
* You can use RouterLink as a property with an array `[routerLink]="['/users']"` (You can add array items without the / for more complex paths)
* RouterLink catches a click on the element, prevents the default reload and analyses what we passed as url, then looks for a fitting route in the configuration
* A relative path (no /) adds the link behind the current path
* A abolsute path (/something) goes right after the dash
* You can use ../ just like folder navigation

### Styling active router links (routerLinkActive)

* `routerLinkActive="active"` If the current route is active, the element will receive the active class
* You can add options to the RouterLinkActive, for example that / isn't always active `[routerLinkActiveOptions]="{exact: true}"` This tells angular to only add the class if it exactly matches the path

### Navigating programmatically (without click a link, with a function or so)

* Import Router from @angular/router in your TS file
* `constructor(private router: Router) { }` With this you can inject the router to use in your Typescript file
* Example of loading a page within a component:
```
export class HomeComponent implements OnInit {

  constructor(private router: Router) { }

  ngOnInit() {
  }

  onLoadServers() {
      // complex calculation or so
      this.router.navigate(['/servers']);
  }

}
```
* The navigate method doesn't know on what path it is, so all paths are handled absolute instead of appended
* `this.router.navigate(['servers'], {relativeTo: this.route});` this is how you can let angular know what the current route is `private route: ActivatedRoute`
* With ActivatedRoute (import/inject required) you can let angular know in your TS file what route you are currently on (default is root url)

### Passing parameters to routes

* `{ path: 'users/:id', component: UserComponent },` In the module you can define a dynamic route which loads a specific id. the : let's angular know this is a dynamic part of the route
* ActivatedRoute can give you information about your route:
```
ngOnInit() {
    this.user = {
      id: this.route.snapshot.params['id'],
      name: this.route.snapshot.params['name']
    };
}
```
With snapshot.params you can get the dynamic part of the url, so `localhost:4200/user/:id/:name` the id and name would be filled with what is in the url
* Then you can use string interpolation to add it in the html:
```
<p>User with ID {{ user.id }} loaded.</p>
<p>User name is {{ user.name }}</p>
```
* Observables allows you to work with async tasks (pieces of code for which you don't know when and if they'll happen)
* Observables allow you to subscribe to an event which might occur in the future, so when it happens you can react
* `this.route.params` is such an observable:
```
this.route.params
  .subscribe(
      (params: Params) => { // this function get's executed whenever the parameters changes
          this.user.id = params['id']; // update the user id/name to the new url
          this.user.name = params['name'];
      }
  );
  ```
  * Observables like this are handy if updates might occur without the component being reinitiated, therefor not able to us ngOnInit
  * Angular cleans up the subscriptions in the component when the component is destroyed
  * With your own observables it is important to unsubscribe OnDestroy() to make
