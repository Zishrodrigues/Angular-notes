# Angular notes

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
  * With your own observables it is important to unsubscribe OnDestroy()

### Query parameters and fragments

* Query parameters are parameters seperated by a questionmark(?) `localhost:4200/users/10/johnny?mode=editing&yes#loading` These are query parameters

#### Pass Query parameters and fragments

* `[queryParams]="{}"` is a bindable property of the RouterLink directive
* `[queryParams]="{allowEdit: '1'}"` This will add `?allowEdit=1` after the url, it can be used to set rights etc
* `fragment="loading"` fragments allow you to add a # behind your url, now after the url a `#loading` will be appended
* You can create such url's in your Typescript file:
```
(click)="onLoadServers(1)"
```
```
onLoadServers(id: number) {
    // complex calculation or so
    this.router.navigate(['/servers', id, 'edit'], {queryParams: {allowEdit: '1'}, fragment: 'loading'});
}
```
This creates `http://localhost:4200/servers/1/edit?allowEdit=1#loading` as url

#### Retrieve Query parameters and fragments

* You need to inject/import Activatedrouter to retrieve Query parameters and the fragment
```
import { ActivatedRoute } from '@angular/router';
```
```
constructor(private serversService: ServersService,
  private route: ActivatedRoute) { }
```
* This is a way to retreive them:
```
console.log(this.route.snapshot.queryParams);
console.log(this.route.snapshot.fragment);
```
This approach only happens when the component is first initialized, so not useable if you change the url after that
```
this.route.queryParams.subscribe();
this.route.fragment.subscribe();
```
This let's you subscribe to the queryParams and fragment, making sure you can react to a change

#### Common gotchas/errors

* Dynamically adding a link:
```
<a
  [routerLink]="['/users', user.id, user.name]"
  href="#"
  class="list-group-item"
  *ngFor="let user of users">
  {{ user.name }}
</a>
```

* Getting the parameter id from the url, converting it to a number and calling a method from the serversService with the id:
```
ngOnInit() {
  const id = +this.route.snapshot.params['id'];
  this.server = this.serversService.getServer(id);
  this.route.params
      .subscribe(
          (params: Params) => {
              this.server = this.serversService.getServer(+params['id']);
          }
      );
}
```

### Child (nested) Routes

* You can declare routes neater instead of using duplicates by using child Routes
normal:
```
const appRoutes: Routes = [
    { path: '', component: HomeComponent }, //localhost:4200/users
    { path: 'users', component: UsersComponent },
    { path: 'users/:id/:name', component: UserComponent },
    { path: 'servers', component: ServersComponent },
    { path: 'servers/:id', component: ServerComponent },
    { path: 'servers/:id/edit', component: EditServerComponent }
];
```
child routes:
```
const appRoutes: Routes = [
    { path: '', component: HomeComponent }, //localhost:4200/users
    { path: 'users', component: UsersComponent, children: [
        { path: ':id/:name', component: UserComponent }
    ] },
    { path: 'servers', component: ServersComponent, children: [
        { path: ':id', component: ServerComponent },
        { path: ':id/edit', component: EditServerComponent }
    ] },
];
```
* Use `<router-outlet></router-outlet>` in your HTML template, child routes will be loaded here
* If you use routing to switch data/views without recreating the component it's important to subscribe to changes in the url parameters
* This code adds /edit to your path relatively to where you are when called:
```
onEdit() {
    this.router.navigate(['edit'], {relativeTo: this.route, queryParamsHandling: 'preserve'});
}
```
More complex routing (going back):
```
this.router.navigate(['../', this.id, 'edit'], {relativeTo: this.route}
```

### Rights based on Query example

HTML for the clickable link:
```
<a
  [routerLink]="['/servers', server.id]"
  [queryParams]="{allowEdit: server.id === 3 ? '1' : '0'}"
  fragment="loading"
  href="#"
  class="list-group-item"
  *ngFor="let server of servers">
  {{ server.name }}
</a>
```
Subscribing to the route change and checking state of allowEdit
```
allowEdit = false;
this.route.queryParams
    .subscribe(
        (queryParams: Params) => {
            this.allowEdit = queryParams['allowEdit'] === '1' ? true : false;
        }
    );
```
Using ngIf to render the correct view
```
<h4 *ngIf="!allowEdit">You're not allowed to edit</h4>
<div *ngIf="allowEdit">
    edit form here
</div>
```
### Configuring / preserving Query parameters when clicking a link

#### queryParamsHandling property

* queryParamsHandling takes a string as a value and you can do things with it
* You can use merge to merge old parameters with new ones ` this.router.navigate(['edit'], {relativeTo: this.route, queryParamsHandling: 'merge'});`
* You can preserve old query parameters ` this.router.navigate(['edit'], {relativeTo: this.route, queryParamsHandling: 'preserve'});`

### 404 error handeling/redirecting

#### Redirecting

* Instead of a component you can enter a redirect url:
```
{ path: 'not-found', component: PageNotFoundComponent},
{ path: '**', redirectTo: '/not-found', pathMatch: 'full'}
```
If you go to `/not-existing-url` it will redirect to `/not-found` (** = wild card route)
* The re-direct url has to be the last Route in your array of Routes (routes get parsed from top to bottom)

### Route module

* When you have multiple routes it's good to use a seperate module for it `app-routing.module.ts`
* Example of a router module:
```
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

import { HomeComponent } from './home/home.component';
import { UsersComponent } from './users/users.component';
import { ServersComponent } from './servers/servers.component';
import { UserComponent } from './users/user/user.component';
import { EditServerComponent } from './servers/edit-server/edit-server.component';
import { ServerComponent } from './servers/server/server.component';
import { PageNotFoundComponent } from './page-not-found/page-not-found.component';

const appRoutes: Routes = [
    { path: '', component: HomeComponent }, //localhost:4200/users
    { path: 'users', component: UsersComponent, children: [
        { path: ':id/:name', component: UserComponent }
    ] },
    { path: 'servers', component: ServersComponent, children: [
        { path: ':id', component: ServerComponent },
        { path: ':id/edit', component: EditServerComponent }
    ] },
    { path: 'not-found', component: PageNotFoundComponent},
    { path: '**', redirectTo: '/not-found', pathMatch: 'full'}
];

@NgModule({
    imports: [
        RouterModule.forRoot(appRoutes)
    ],
    exports: [RouterModule]
})
export class AppRoutingModule {

}
```
It has to be imported to your main app module, add `AppRoutingModule` in the imports array and import the class `import { AppRoutingModule } from './app-routing.module';`

### Route Guards (protecting routes)

* Route Guards are functionality/logic/code which is executed before a route is loaded or once you want to leave a router
* For example checking if a user is logged in before giving them access to a specific route

#### canActivate guard

* Guards are services, they are a specific feature to guard routes but in the end you set them up like you would a service `auth-guard.service.ts`
* In the routes module you need to define which routes are protected by a specific guard:
```
import { AuthGuard } from './auth-guard.service';

{ path: 'servers', canActivate: [AuthGuard], component: ServersComponent, children: [
    { path: ':id', component: ServerComponent },
    { path: ':id/edit', component: EditServerComponent }
] }
```
The services need to be declared in your main app module `providers: [ServersService, AuthService, AuthGuard],`

* Guard service example:
```
import {
    CanActivate,
    ActivatedRouteSnapshot,
    RouterStateSnapshot,
    Router
} from '@angular/router';
import { Observable } from 'rxjs/Observable';
import { Injectable } from '@angular/core';

import { AuthService } from './auth.service';

@Injectable()
export class AuthGuard implements CanActivate {
    constructor(private authService: AuthService, private router: Router) {}

    canActivate(route: ActivatedRouteSnapshot,
                state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
        return this.authService.isAuthenticated()
            .then(
                (authenticated: boolean) => {
                    if (authenticated) {
                        return true;
                    } else {
                        this.router.navigate(['/']);
                    }
                }
            );
    }
}
```

##### Protecting child (nested) routes with canActivate

* Adding the CanActivateChild interface in the guard allows you to use it in your Routes
```
canActivateChild(route: ActivatedRouteSnapshot,
            state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
    return this.canActivate(route, state);
}
```
Now you can use `canActivateChild: [AuthGuard],` instead of just canActivate to protect the child Routes

#### canDeactivate guard

* canDeactivate contols wether you are allowed to leave a route or not
* An interface is a contract which can be imported by some other class and forces that class to provide some logic:
```
import { Observable } from 'rxjs/Observable';
import { CanDeactivate, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';

export interface CanComponentDeactivate {
    canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
}

export class canDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {

    canDeactivate(component: CanComponentDeactivate,
        currentRoute: ActivatedRouteSnapshot,
        currentState: RouterStateSnapshot,
        nextState?: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
            return component.canDeactivate();
        }
}
```
Now if you call canDeactivate from a component, you're sure it has the logic of the interface which it needs to pass the right component

#### Passing data to a route (once it is loaded)

* If you have a dynamic error message page, for example route is not found, you need to be able to pass that data
##### Passing static data to a route
```
ngOnInit() {
  //   this.errorMessage = this.route.snapshot.data['message'];
    this.route.data.subscribe(
        (data: Data) => {
            this.errorMessage = data['message'];
        }
    );
}
```
and in your router module:
```
{ path: 'not-found', component: ErrorPageComponent, data: {message: 'Page not found!'}},
```
##### Passing dynamic data to a route (resolve Guard)

* The resolver Guard will not decide whether the component should be loaded or not, it will always render the component. It will do some preloading, fetch some data the component will need
* This is for loading data before you display a route
Route module:
```
{ path: ':id', component: ServerComponent, resolve: {server: ServerResolver} }
```
Component Typescript:
```
ngOnInit() {
    this.route.data
      .subscribe(
          (data: Data) => {
              this.server = data['server'];
          }
      );
}
```
### Location strategies / route fallback

* On a live app the url is always handled by the server first, so the local url's you set up might not work out of the box
* The server has to be set up in a way that in case of a 404, the server returns the index file, the file holding the Angular app
* The server looks for files that matches the url, but you only have 1 file; your index.html which contains your angular app
* For older browsers you can fallback to using a # hash as url instead of / dash `RouterModule.forRoot(appRoutes, {useHash: true})`
* The Default for `RouterModule.forRoot(appRoutes, {useHash: true})` is false

## Section 13: Observables

* An Observable can be thought of as a data source
* You have an Observable and an observer, and in between there is a stream/timeline. In this timeline there can be multiple events emitted by the observable or 'data packages'
* So the observable can emit data because you trigger it to do so programmatically, it can be connected to a button (user input) or an http request etc
* The observer is your code (the subscribe function). You have three ways to handle data. 1) Handle data normally 2) Handle error 3) handle completion
* Those are the 3 types of data packages you can receive (data,error,completion)
* In these hooks/boxes your code gets executed. You can define what happens in each situation. (An observable doesn't have to complete)
* You use it to handle a sync tasks because user inputs, https request etc are async tasks. You don't know when they will happen or how long they will take
* So instead of waiting for the completion for these events(thus blocking your code) we continue in our file and use Observables to keep an eye on when something happens
* Observables are operators, giving them a major advantage over callbacks
* So the Observable might emit a normal data package, it might emit an error or a completion, and the respective code will be executed

### Built-in Angular observables

* Params is an observables Angular has to check parameter changes in your url, thus giving you a change to react to these changes
* Here you use params to check for a change in the url, and then update the id:
```
id: number;
ngOnInit() {
  this.route.params
    .subscribe(
      (params: Params) => {
        this.id = +params['id'];
      }
    );
}
```
This is the receiving(observer part/ subscriber) part, here we handle the data and react accordingly

### Custom/own Observables

* To create your own Observables you need to import:
```
import { Observable } from 'rxjs/Observable';
import 'rxjs/Rx';
```

* This is an Observable that emits a number every second and an observer that logs it:
```
const myNumbers = Observable.interval(1000);
myNumbers.subscribe(
    (number: number) => {
        console.log(number);
    }
);
```
* `.create` create takes an argument and this function should hold your async code
* An custom Observable and Observer:
```
const myObservable = Observable.create((observer: Observer<string>) => {
    setTimeout(() => {
        observer.next('first package');
    }, 2000);
    setTimeout(() => {
        observer.next('second package');
    }, 4000);
    setTimeout(() => {
        // observer.error('error package');
        observer.complete();
    }, 5000);
});
myObservable.subscribe(
    (data: string) => { console.log(data); },
    (error: string) => { console.log(error); },
    () => { console.log('completed'); }
);
```

### Unsubscribe

* If an observable isn't completed automatically and keeps going, and you keep being subscribed then it can create bugs after the component is destroyed (leaving page etc)
* Angular unsubscribes automatically from it's own Observables (params) but you have to do this for custom observables
* You need to use onDestroy for this:
```
import { Component, OnInit, OnDestroy } from '@angular/core';
```
```
export class HomeComponent implements OnInit, OnDestroy {
```
```
ngOnDestroy() {

}
```
* To unsubscribe you create a var where you hold your sub, then destroy it:
```
customObsSubscription: Subscription;
```
```
this.customObsSubscription = myObservable.subscribe(
    (data: string) => { console.log(data); },
    (error: string) => { console.log(error); },
    () => { console.log('completed'); }
);
```
```
ngOnDestroy() {
    this.customObsSubscription.unsubscribe();
}
```

### More about Observables

* [RxJS](www.reactivex.io)
* www.reactivex.io (RxJS)

### Subject

* A subject is like an observable but it allows you to conveniently push it to emit new data during your code
* A subject is observable and observer at the same time
* It's good practice to use a subject instead of event emitter for cross component communication
```
onActivate() {
    this.usersService.userActivated.next(this.id);
}
```
```
this.usersService.userActivated.subscribe(
    (id: number) => {
        if (id === 1) {
            this.user1Activated = true;
        } else if (id === 2) {
            this.user2Activated = true;
        }
    }
);
```

### Observable operators

* RXJS Operators allow you to transform the data you receive to something else, and still stay inside the observable
* Import `import 'rxjs/Rx';` to unlock operators
* This is the Operator `.map` which transforms/maps data into something else:
```
const myNumbers = Observable.interval(1000)
  .map(
      (data: number) => {
          return data * 2;
      }
  );
```

## Section 15: Handeling Forms in Angular apps

* Because Angular is a one page app there is no submitting to the server like you normally would. Instead you will need to handle the form through Angular
* You can reach out through Angulars HTTP service to the server for form submitting
* Angular allows you to get and check values for forms, validation etc
* Angular gives you a Javascript object representation of your form, making it simple to retrieve user values and work with them
* Angular offers 2 approaches to handle forms. Template driven and reactive

### Template driven forms introduction

* You set up your form in the HTML template and Angular will automatically infer the structure of your form (which controls, inputs etc)
* Angular infers the Form Object from the DOM

### Reactive forms introduction

* Here you define the structure of the form in Typescript code, you also set up the HTML code and you manually connect these. Gives you greater control and fine tuning
* Form is created programmatically and synchronized with the DOM

### Template driven forms

* The <form> element doesn't have an action, submit. You don't want it to submit when clicked. Instead Angular should handle the form

#### Creating the form and registering the controls

* Make sure you import the form module `import { FormsModule } from '@angular/forms';` and have it as import:
```
imports: [
  BrowserModule,
  FormsModule,
  HttpModule
],
```
* When Angular detecs a <form> element in the HTML code it will automatically create a javascript representation of the form
* So the <form> element serves as a selector for a directive which creates the javascript form object for you
* Angular will not automatically detect your inputs in your form, you might not want every input in your javascript form object (dropdown etc)
* You need to register controls manually, tell Angular what to represent in Javascript
* With ngModel you can tell Angular that this input is a control, the `name=""` tells Angular the name of the input:
```
<label for="username">Username</label>
<input
    type="text"
    id="username"
    class="form-control"
    ngModel
    name="username">
```
* To submit a form you add `(ngSubmit)=""` to the form and call a method:
```
      <form (ngSubmit)="onSubmit(f)" #f="ngForm">
```
The method can be in your TS file, `#f="ngForm"` is the reference to the js form Angular created
```
onSubmit(form: HTMLFormElement) {
    console.log(form)
}
```
* The JS form object has a lot of properties which give you information about the form (disabled, enabled, errors etc)

##### Accessing the form with @ViewChild

* `@ViewChild('f') signupForm: NgForm;` lets you store the form object
```
onSubmit() {
    console.log(this.signupForm);
}
```
* This is useful if you need to access the form not only at the time of submit, but also earlier

##### Controlling the validity of the form (validation)

* Validation should always also happen on the server, but you can enhance UX by also implementing it in the frontend
* `required` is a HTML attribute you can add to a input, Angular however will detect it and will automatically configure the form to make sure that the input is invalid if empty
* Same goes for email, but you also have the `email` attribute (not vanilla HTML, Angular directive):
```
<input
    type="email"
    id="email"
    class="form-control"
    ngModel
    name="email"
    required
    email>
```
* In the `valid` property of the form object you can see if the form is validated or not (true/false)
* This is not only true on form level, but also per control level (you can see specifically if the email is valid or not)
* Angular adds classes on input. `ng-valid ng-dirty ng-touched` these classes give us information about the state of the individual controls
* https://angular.io/docs/ts/latest/api/forms/index/Validators-class.html are the built in validators that ship with angular
* https://angular.io/api?type=directive See the needed directives
* `pattern="^[1-9]+[0-9]*$"` (has to be number greater than 0)
* You might want to enable HTML 5 validation, Angular enables it. You enable this by adding `ngNativeValidate` to a control in your HTML template

* You can disable the submit button if the form is invalid by accessing the local reference:
```
<button
    class="btn btn-primary"
    type="submit"
    [disabled]="!f.valid">Submit</button>
```
* You can style the addes css classes to give feedback to the user on validation:
```
input.ng-invalid.ng-touched {
    border: 1px red solid;
}
```

###### Displaying error messages/help

* Using local references you can determine if an input is invalid and display an error message accordingly:
```
<div class="form-group">
  <label for="email">Mail</label>
  <input
      type="email"
      id="email"
      class="form-control"
      ngModel
      name="email"
      required
      email
      #email="ngModel">
      <span class="help-block" *ngIf="!email.valid && email.touched">Please enter a valid email!</span>
</div>
```

##### Setting default values with ngModel / property binding (one-way)

* In your Typescript file:
```
  defaultQuestion = 'pet';
```
in the html:
```
<select
    id="secret"
    class="form-control"
    [ngModel]="defaultQuestion"
    name="secret">
  <option value="pet">Your first Pet?</option>
  <option value="teacher">Your first teacher?</option>
</select>
```
Now the default selected value is "Your first pet?"
* This would work for the username etc

###### Two-way binding in forms

* If you want to instantly check something or repeat what the user entered
* Typescript file: `answer = '';`
HTML:
```
<div class="form-group">
    <textarea
        name="questionAnswer"
        rows="3"
        class="form-control"
        [(ngModel)]="answer">
        </textarea>
</div>
<p>Your reply: {{ answer }}</p>
```

##### Grouping form Controls

* You might want to group form controls to create structure in your form object, grouping certain values
* You could then validate individual groups
* Using `ngModelGroup` you can group form controls, you need to give it a name like userData `ngModelGroup="userData"`
* You can show an error message for this group:
```
<div
    id="user-data"
    ngModelGroup="userData"
    #userData="ngModelGroup">
```
```
<p *ngIf="!userData.valid && userData.touched">User Data is invalid!</p
```
##### Handeling radio buttons

* Create a genders array in your TS file `genders = ['male', 'female'];`
HTML:
```
<div class="radio" *ngFor="let gender of genders">
    <label>
        <input
            type="radio"
            name="gender"
            ngModel
            [value]="gender"
            required>
            {{ gender }}
    </label>
</div>
```

##### Setting and patching form values

TS:
```
suggestUserName() {
  const suggestedName = 'Superuser';
  this.signupForm.setValue({
      userData: {
          username: suggestedName,
          email: ''
      },
      secret: 'pet',
      questionAnswer: '',
      gender: 'male'
  });
}
```
HTML:
```
<button
    class="btn btn-default"
    type="button"
    (click)="suggestUserName()">Suggest an Username</button>
```
On click the value of Username will be Superuser, however this will reset the other fields. This is for a specific input:
```
suggestUserName() {

  this.signupForm.form.patchValue({
      userData: {
          username: suggestedName
      }
  });
}
```
`PatchValue()` is only available on the form wrapped by ngForm itself

#### Using form data (extracting data and using it)

* Showing the data from your form:
Typescript:
```
user = {
    username: '',
    email: '',
    secretQuestion: '',
    answer: '',
    gender: ''
};
submitted = false;
```
```
onSubmit() {
    this.submitted = true;
    this.user.username = this.signupForm.value.userData.username;
    this.user.email = this.signupForm.value.userData.email;
    this.user.secretQuestion = this.signupForm.value.secret;
    this.user.answer = this.signupForm.value.questionAnswer;
    this.user.gender = this.signupForm.value.gender;
}
```
HTML:
```
<div class="row" *ngIf="submitted">
    <div class="col-xs-12">
    <h3>Your data</h3>
    <p>Username: {{ user.username }}</p>
    <p>Mail: {{ user.email }}</p>
    <p>Secret Question: {{ user.secretQuestion }}</p>
    <p>Answer: {{ user.answer }}</p>
    <p>Gender: {{ user.gender }} </p>
    </div>
</div>
```

#### Resetting forms

* You can reset the form using `this.signupForm.reset();`
* This will not only reset the values, but also the states (valid, touched etc) as if the page was reloaded

### Reactive forms

* In the reactive approach the form is created programmaticaly, in Typescript code
* To setup a form you need to import form group `import { FormGroup } from '@angular/forms';` and setup a form property `signupForm: FormGroup;`
* In your app.module you need to import the ReactiveFormsModule which contains the needed tools `import { ReactiveFormsModule } from '@angular/forms';`
```
imports: [
  BrowserModule,
  ReactiveFormsModule,
  HttpModule
]
```

#### creating a reactive form in code

* Initialize the form before the template is rendered using a lifecycle hook (ngOnInit):
```
signupForm: FormGroup;

ngOnInit() {
    this.signupForm = new FormGroup({

    });
}
```
This is a basic empty form with no controls

* Controls are key value pairs we pass to the overal control `FormGroup`
* Form:
HTML:
```
<form>
  <div class="form-group">
    <label for="username">Username</label>
    <input
      type="text"
      id="username"
      class="form-control">
  </div>
  <div class="form-group">
    <label for="email">email</label>
    <input
      type="text"
      id="email"
      class="form-control">
  </div>
  <div class="radio" *ngFor="let gender of genders">
    <label>
      <input
        type="radio"
        [value]="gender">{{ gender }}
    </label>
  </div>
  <button class="btn btn-primary" type="submit">Submit</button>
</form>
```
Typescript:
```
signupForm: FormGroup;

ngOnInit() {
    this.signupForm = new FormGroup({
        'username': new FormControl(null),
        'email': new FormControl(null),
        'gender': new FormControl('male')
    });
}
```

##### Syncing HTML and Form object

* Using `[formGroup]="signupForm"` you tell Angular not to create a form by itself, but use your set up form `<form [formGroup]="signupForm">`
* With `formControlName=""` you can tell Angular what the name of the control in your typescript form is:
```
<input
  type="text"
  id="username"
  formControlName="username"
  class="form-control">
```

##### Submitting the forms

* `<form [formGroup]="signupForm" (ngSubmit)="onSubmit()">` This adds a submit method
Typescript:
```
onSubmit() {
    console.log(this.signupForm);
}
```

##### Reactive form validation

* You don't configure the form in the template, you only sync it to your TS code
* You can configure the validators in the TS object:
```
ngOnInit() {
    this.signupForm = new FormGroup({
        'username': new FormControl(null, Validators.required),
        'email': new FormControl(null, [Validators.required, Validators.email]),
        'gender': new FormControl('male')
    });
}
```

* Using `get()` you can set a validation/help message, by getting access to a control in your form:
```
<input
  type="text"
  id="username"
  formControlName="username"
  class="form-control">
<span
    class="help-block"
    *ngIf="!signupForm.get('username').valid && signupForm.get('username').touched">Please enter a valid username!</span>
```
General form message:
```
<span
    class="help-block"
    *ngIf="!signupForm.valid && signupForm.touched">Please enter a valid data!</span>
```

* Css classes for validation just work (ng-touched, ng-valid etc)

##### Grouping controls in reactive forms

* You can nest form groups:
TS:
```
ngOnInit() {
    this.signupForm = new FormGroup({
        'userData': new FormGroup({
            'username': new FormControl(null, Validators.required),
            'email': new FormControl(null, [Validators.required, Validators.email])
        }),
        'gender': new FormControl('male')
    });
}
```
HTML:
```
<div formGroupName="userData">
    <div class="form-group">
      <label for="username">Username</label>
      <input
        type="text"
        id="username"
        formControlName="username"
        class="form-control">
        <span
            class="help-block"
            *ngIf="!signupForm.get('userData.username').valid && signupForm.get('userData.username').touched">Please enter a valid username!</span>
    </div>
    <div class="form-group">
      <label for="email">email</label>
      <input
        type="text"
        id="email"
        formControlName="email"
        class="form-control">
        <span
            class="help-block"
            *ngIf="!signupForm.get('userData.email').valid && signupForm.get('userData.email').touched">Please enter a valid email!</span>
    </div>
</div>
```
##### Arrays of form controls (reactive)

* You can create an array of controls dynamically:
HTML:
```
<div formArrayName="hobbies">
    <h4>Your Hobbies</h4>
    <button
        class="btn btn-default"
        type="button"
        (click)="onAddHobby()">Add Hobby</button>
        <div
            class="form-group"
            *ngFor="let hobbyControl of signupForm.get('hobbies').controls; let i = index">
            <input type="text" class="form-control" [formControlName]="i">
        </div>
</div>
```
Typescript:
```
ngOnInit() {
    this.signupForm = new FormGroup({
        'userData': new FormGroup({
            'username': new FormControl(null, Validators.required),
            'email': new FormControl(null, [Validators.required, Validators.email])
        }),
        'gender': new FormControl('male'),
        'hobbies': new FormArray([])
    });
}

onAddHobby() {
    const control = new FormControl(null, Validators.required);
    (<FormArray>this.signupForm.get('hobbies')).push(control);
}
```
You have to cast `(<FormArray>this.signupForm.get('hobbies')).push(control);` the array type so it knows it's an array

##### Custom validators (reactive)

* Custom validators can be good in specific cases, like if there is a certain username you don't want people to use
* A validator is merely a method angular uses whenever you validate a control, and on change it will check that control
* You have to create an array ` forbiddenUsernames = ['Chris', 'Anna'];`
* If validation is succesful you have to pass nothing or null
* Creating a custom form validator:
```
forbiddenNames(control: FormControl): {[s: string]: boolean} {
    if (this.forbiddenUsernames.indexOf(control.value) !== -1) {
        return {'nameIsForbidden': true};
    }
    return null;
}
```
Then you add it in the form object `'username': new FormControl(null, [Validators.required, this.forbiddenNames.bind(this)]),` you have to bind `this`

##### Using error codes (reactive)

* Angular adds the error codes on the individual controls in the errors object
* Error codes can be used to show the right error messages:
```
<span
    class="help-block"
    *ngIf="!signupForm.get('userData.username').valid && signupForm.get('userData.username').touched">
        <span *ngIf="signupForm.get('userData.username').errors['nameIsForbidden']">This name is invalid!</span>
        <span *ngIf="signupForm.get('userData.username').errors['required']">This field is required!</span>
</span>
```

##### Custom Async Validators

* Sometimes you need a validator which is able to wait for a response from the server before letting you know if it is valid or not
* Setting up a async validator (timeout is to fake server fetch time):
```
forbiddenEmails(control: FormControl): Promise<any> | Observable<any> {
    const promise = new Promise<any>((resolve, reject) => {
        setTimeout(() => {
            if (control.value === 'test@test.com') {
                resolve({'emailIsForbidden': true});
            } else {
                resolve(null);
            }
        }, 1500)
    });
    return promise;
}
```
In your form object `'email': new FormControl(null, [Validators.required, Validators.email], this.forbiddenEmails)` `this` needs to be binded if you plan to use it
* While it is waiting to be validated the class `ng-pending` is added to the input

##### Reacting to status or value changes

* ValueChanges:
```
this.signupForm.valueChanges.subscribe(
    (value) => console.log(value)
);
```
* StatusChanges:
```
this.signupForm.statusChanges.subscribe(
    (value) => console.log(value)
);
```
* These hooks can be used to react more closely to what's happening in the form

##### Setting and patch values (reactive)

* Setting the values:
```
this.signupForm.setValue({
    'userData': {
        'username': 'max',
        'email': 'max@test.com'
    },
    'gender': 'male',
    'hobbies' : []
});
```
* Setting a specific value:
```
this.signupForm.patchValue({
    'userData': {
        'username': 'max'
    }
});
```
* You can reset the whole form using ` this.signupForm.reset();` (can also hold specific inputs)

## Section 17: Pipes

* Pipes are a feature built into Angular 2
* Pipes allow you to transform output in your template
* There are pipes for different types of output, and for sync and async data

### A basic example of pipes

* You have a username, that's a property in your component. It holds a string. You output a string using interpolation
```
username = 'Max'
```
```
<p>{{ username }}</p>
```
* You decide that it would be nice if the string was only uppercase, but only when you output it (the property stays the same)
* For this you can use the uppercase pipe(built in pipe):
```
<p>{{ username | uppercase }}</p>
```
The output would now be uppercase `MAX`

* This is the main purpose of pipes, transforming values

### Using pipes

* The uppercase pipe makes text uppercase `{{ server.instanceType | uppercase}}`
* You can change the date using the date pipe `{{ server.started | date}}`

#### Configuring pipes (adding parameters)

* You can configure pipes with parameters to change the output
* `{{ server.started | date:'fullDate' }}` This changes the date format to a full Date
* You add paremters with `:` for example `{{ server.started | date:'PARAMETER':'PARAMETER2' }}`

#### Learning more about pipes

* https://angular.io/api?query=pipe here you can see the pipes built into Angular

#### Chaining/combining multiple pipes

* You can chain pipes by putting a pipe `|` symbol between them `{{ server.started | date:'fullDate' | uppercase }}`
* The order is important (eg: you can't uppercase a date before it's turned into a string by the date pipe)
* Apply the pipes in the order you want to transform your output

### Creating custom pipes

* Create a file for the pipe `shorten.pipe.ts` using the naming convention
* Import the PipeTransform interface:
```
import { PipeTransform, Pipe } from '@angular/core';

@Pipe({
    name: 'shorten'
})
export class ShortenPipe implements PipeTransform {
    transform(value: any) {
        if (value.length > 10) {
            return value.substr(0, 10) + ' ...';
        } return value;
    }
}
```
A pipe that returns the first 10 characters of a string, using the imported `@Pipe()` decorator you can name it and use it in your html template

* Transform always needs to return something. A pipe is you put something in you put something out, thus the name Pipe
* You need to add the pipe to your app.module:
```
import { ShortenPipe } from './shorten.pipe';
```
```
@NgModule({
  declarations: [
    AppComponent,
    ShortenPipe
  ]
```
* Call the Pipe in your html `{{ server.name | shorten }}`

##### Custom pipe with parameters

* You can create a custom pipe with parameters that allow the user to specify the number of characters for example:
```
import { PipeTransform, Pipe } from '@angular/core';

@Pipe({
    name: 'shorten'
})
export class ShortenPipe implements PipeTransform {
    transform(value: any, limit: number) {
        if (value.length > limit) {
            return value.substr(0, limit) + ' ...';
        } return value;
    }
}
```
HTML:
```
{{ server.name | shorten:'20' }}
```

* You can add parameters by adding types in your transform method

#### Advanced custom Pipe

* `ng g p pipename` allows you to generate a pipe in the cli
* A pipe which filters an array based on a string:
```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter'
})
export class FilterPipe implements PipeTransform {

  transform(value: any, filterString: string, propName: string): any {
    if (value.length === 0) {
        return value;
    }
    const resultArray = [];
    for (const item of value) {
        if (item[propName] === filterString) {
            resultArray.push(item);
        }
    }
    return resultArray;
  }
}
```
In your html you filter based on input:
```
<input type="text" [(ngModel)]="filteredStatus">
```
```
*ngFor="let server of servers | filter:filteredStatus:'status'"
```
* Pipes can be used on all output data, so also in the template loops

### Pure and impure Pipes

* Angular doesn't rerun the pipe whenever the data(objects / arrays) changes, this can cause issues in some cases
* If you put pure to false, then the pipe gets rerun whenever data changes, be aware that this can cause performance issues as it reruns every time some data changes on the page
```
@Pipe({
  name: 'filter',
  pure: false
})
```
The default is `pure: true`

### Async Pipe

* `async` pipe recognizes if something is a promise or an observable, and it print the data to the screen on change

## Section 18: HTTP requests

* We have a SPA so the HTTP requests happen through AJAX, so that we don't need a new page when receiving the JSON response

### Sending requests (eg post request)

* Your app module needs to have the Http module imported
* Import Angular http `import { Http } from '@angular/http';` and `constructor(private http: Http) {}`
* The request service:
```
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';

@Injectable()
export class ServerService {
    constructor(private http: Http) {}
    storeServers(servers: any[]) {
        return this.http.post('https://udemy-ng-http-52335.firebaseio.com/', servers);
    }
}
```
At this point it's not sending a request yet

* Angular Http creates an observable when you do a request, it won't send the request as long as there is no subscription to it
* This calls the request service and logs the response:
```
onSave(){
    this.serverService.storeServers(this.servers)
      .subscribe(
          (response) => console.log(response),
          (error) => console.log(error)
      );
}
```

#### Adjusting request headers

```
storeServers(servers: any[]) {
    const headers = new Headers({
        'Content-Type': 'application/json'
    });
    return this.http.post('https://udemy-ng-http-52335.firebaseio.com/data.json', servers, {headers: headers});
}
```

### GET Requests

* In your request service:
```
getServers() {
    return this.http.get('https://udemy-ng-http-52335.firebaseio.com/data.json');
}
```
In the Typescript file:
```
onGet() {
    this.serverService.getServers()
      .subscribe(
          (response: Response) => {
              const data = response.json()
              console.log(data);
          },
          (error) => console.log(error)
      );
}
```
The Angular Respons import let's you unwrap the data and make it into a Javascript Object

### Transforming data with Observables

* You can make sure the request service gets the data before sending it to the component
Service:
```
getServers() {
    return this.http.get('https://udemy-ng-http-52335.firebaseio.com/data.json')
        .map(
            (response: Response) => {
                const data = response.json();
                return data;
            }
        );
}
```
Typescript:
```
onGet() {
    this.serverService.getServers()
      .subscribe(
          (servers: any[]) => console.log(servers),
          (error) => console.log(error)
      );
}
```

### Using the returned data

* Adding something to the name of the servers after fetch:
```
getServers() {
    return this.http.get('https://udemy-ng-http-52335.firebaseio.com/data.json')
        .map(
            (response: Response) => {
                const data = response.json();
                for (const server of data) {
                    server.name = 'FETCHED_' + server.name;
                }
                return data;
            }
        );
}
```

### Catching HTTP errors

```
getServers() {
    return this.http.get('https://udemy-ng-http-52335.firebaseio.com/data')
        .map(
            (response: Response) => {
                const data = response.json();
                for (const server of data) {
                    server.name = 'FETCHED_' + server.name;
                }
                return data;
            }
        )
        .catch(
            (error: Response) => {
                console.log(error)
                return Observable.throw(error);
            }
        );
}
```
or `return Observable.throw('Something went wrong!');`

### Async pipes with HTTP requests

* You can connect a property `appName = this.serverService.getAppName();` to a request and use async pipe to update it `{{ appName | async }}`

## Section 20: Authentication & Route protection (Oauth)

* In a traditional web app the server is responsible for sending a complete html code to the client, in a SPA the client is responsible for making sure the HTML changes without receiving templates
* In a traditional web app the session is stored on the server and the client gets a session cookie, which stores the id of the session, which can be sent with every request
* In a SPA we send the Auth information to the server, but a session isn't stored. The server sends back a Token which is hashed with a secret, with this token the client can access protected resources on the server
* More about the token https://jwt.io/introduction/


## Section 21: Angular Modules & Optimizing apps

* Your Angular app exists of Components, directives and services etc. All these have to be registered in a module or multiple modules
* The idea behind this is that you tell angular what your app consists of; which components to you use, which directives/services
* Angular doesn't automatically scan and add your files. This makes performance better because it doesn't use what you don't need
* Modules bundle functionality and let you import them

### The App module

* An import on your module is a Typescript feature. Typscript needs to know where a specific thing (eg class) you use lives, it's for Typscript not Angular
* Webpack will go through these imports and bundle all of them when building
* Angular modules define how our app looks like to angular
* When your App Module has tons of imports and declarations you can improve it by using multiple modules

#### declarations array

* In the declarations array we define which components, directives or pipes our app(this module) uses

#### imports array

* In imports we define which other modules does this module use. Here you also import built in modules like `BrowserModule` and `FormsModule`

#### exports array

* What you put in exports can be imported by another module to use
* This includes all the directives etc
* bundle of all the module functionality that you can import

#### providers array

* Everything we provide here will be provided for the whole application, which means you can use one instance for the behavior of the whole app

#### bootstrap array

* Here you define the root component, the main component where you start registering all the elements you use (usually app component)

### Feature Modules (custom module)

* A custom module could be a feature module, for a specific feature
* When you use a module for a feature you can quickly see what the feature relies on, what it uses etc
* Good enhancement from a code structuring perspective

* Defining a module in `recipes.module.ts`
```
import { NgModule } from '@angular/core';

@ngModule()
export class RecipesModule {}
```

* In most cases you don't use a Service to a feature model because it's used throughout the app
* Every feature module needs the CommonModule in imports, this gives you access to the common directives like ngClass, ngIf, and changes are high that you'll need some of those
* The main module has the BrowserModule instead of CommonModule, BrowserModule has some stuff Angular needs on start up, only your main module should have this
* You can't duplicate declarations in multiple modules
* Router forRoot must only be called in the root/app module, otherwise use forChild
```
@NgModule({
    imports: [
        RouterModule.forChild(recipesRoutes)
    ],
    exports: [RouterModule]
})
```

### Shared modules

* A shared module is a module not containing a feature, but containing something that will be shared across multiple other modules
* Since you can't import the same directive in multiple models, you can use a shared model
```
import { NgModule } from '@angular/core';

import { DropdownDirective } from './dropdown.directive';

@NgModule({
    declarations: [
        DropdownDirective
    ],
    exports: [
        DropdownDirective
    ]
})
export class SharedModule {}
```

### Modules and routing (lazy loading) / increase performance

* You might not need the code for all your features if the user doesn't visit certain pages, lazy loading means that you can only load code when it is needed
* The Module will only be loaded if you visit a route that can lead to that module
* Removing the component from the main module and adding loadChildren to the route allows lazy loading `{ path: 'recipe', loadChildren: './recipes/recipe.module#RecipesModule'},`

### Modules and Service Injection

* Is you provide a Service on multiple modules that aren't lazy loaded, they will be combined by angular to a Root injector. Which creates one instance of that Service for those modules
* A lazy loaded module can still use the same instance of a Service, but if it provides it's own Service in it's providors array it will get a new instance (child injector) of the Service
* So whether you load a module lazily or not can change how many Instances of a Service you're going to use
* You should avoid adding a Service to a shared module's providors array, this creates a child injector
* Don't add providors on a shared module

### Core module

* Things that you really only need on start up can be added to a core module
* The core module will only be imported by the app module, this keeps the app module cleaner
* It's good to only have the AppComponent in your app module declarations, this means your modules are clean, the core module can import the other components you need

### Using Ahead-of-time Compilation

* Angular compiles your HTML templates to Javascript
* Angular offers two types of compiling your code

#### Just-in-time compilation

* Here you develop your code -> then ship it(gets compiled) -> app downloaded to browser -> Angular bootstraps the app (in this step it parses and compiles the templates to JS)

#### Ahead-in-time compilation

* Here you develop your code -> Then Angular parses and compiles templates to JS -> ship it to production/compile -> download to browser
* The advantages to this is that the app starts faster, in browser compiling isn't needing
* Templates get checked during development, or right after (errors you'd see in your js console are now seen in your build process)
* Smaller file size as unused Features can be stripped out and the compiler itself isn't shipped

* Build for production: `ng build --prod`
* Build for production and ahead of time compilation: `ng build --prod --aot`
* The dist folder is created once you run ng build (main file = app code)

### preloading lazy loading

* Because lazy loading loads the component when you go to the route you might have a second where the app hangs because it's loading
* You can avoid this by preloading while the user is on the app
* To preload all your lazy modules after the app has been loaded, add it in the route module imports:
```
import { Routes, RouterModule, PreloadAllModules } from '@angular/router';
```
```
@NgModule({
  imports: [RouterModule.forRoot(appRoutes, {preloadingStrategy: PreloadAllModules})],
  exports: [RouterModule]
})
```

## Section 22: Deployment

### Deployment preparations and Important steps

1. Build the app for Production (minify the code, consider AoT compliation) `ng build --prod --aot` with CLI
2. Set the correct <base> element if on a after hash url eg: `example.com/my-app` you should have <base href="/my-app/">
3. Make sure your Servers always returns index.html, return index.html in case of 404 errors (angular handles the routes, not the server)

* You can deploy the files in your `dist` folder

## Section 23: Angular Animations

* Angular ships with it's own animation system (attaching/detaching animations etc)
* In the component decorator you define the animations that component should be aware of:
```
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  animations: [

  ]
})
```

* Angular animations work from transitioning from state 1 to state 2

#### trigger

* With trigger() `import { trigger, state, style, transition, animate } from '@angular/animations';` we tell angular that certain elements that can be placed in our DOM, if they are placed, it should trigger a certain animation
HTML:
```
<button class="btn btn-primary" (click)="onAnimate()">Animate!</button>
<div [@divState]="state"></div>
```
TS:
```
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  animations: [
      trigger('divState', [
          state('normal', style({
              'background-color': 'red',
              transform: 'translateX(0)'
          })),
          state('highlighted', style({
              'background-color': 'blue',
              transform: 'translateX(100px)'
          })),
          transition('normal => highlighted', animate(300)),
          transition('highlighted => normal', animate(500)),
      ])
  ]
})
```
The state() represents the first state and the second state, the transition defines how to animate it
```
onAnimate() {
    this.state == 'normal' ? this.state = 'highlighted' : this.state = 'normal';
}
```
the on click method that will change the state and trigger the animation

* `transition('normal <=> highlighted', animate(300))` let's you use the same timing
* More complex trigger:
```
trigger('wildState', [
    state('normal', style({
        'background-color': 'red',
        transform: 'translateX(0) scale(1)'
    })),
    state('highlighted', style({
        'background-color': 'blue',
        transform: 'translateX(100px) scale(1)'
    })),
    state('shrunken', style({
        'background-color': 'green',
        transform: 'translateX(0) scale(0.5)'
    })),
    transition('normal => highlighted', animate(300)),
    transition('highlighted => normal', animate(500)),
    transition('shrunken <=> *', [
        style({
            'background-color': 'orange'
        }),
        animate(1000, style({
            borderRadius: '50px'
        })),
        animate(500)
    ])
])
```
* The `[@wildState]="wildState"` defines what animation is played
* You can give a transition an array with the different states in the transition to finetune it

### Void state

* `void` is a reserved state by Angular which represents an element which wasn't added to the DOM in before the animations
```
[@list1]
```
```
trigger('list1', [
    state('in', style({
        opacity: 1,
        transform: 'translateX(0)'
    })),
    transition('void <=> *', [
        style({
            opacity: 0,
            transform: 'translateX(-100px)'
        }),
        animate(300)
    ])
])
```
The style in the transition is the first state after the void adds the element to the html, it will then animate to the final state

### Animation keyframes

```
import { trigger, state, style, transition, animate } from '@angular/animations';
```
```
transition('void => *', [
    animate(300, keyframes([
    style({
        opacity: 0,
        transform: 'translateX(-100px)',
        offset: 0
    }),
    style({
        opacity: 0.5,
        transform: 'translateX(-50px)',
        offset: 0.7
    }),
    style({
        opacity: 1,
        transform: 'translateX(0)',
        offset: 1
    }),
    ]))
])
```

### Group animations

* With the group method (needs to be imported) you can pass an array of animations you want to perform in sync (at the same time)

### Animation callbacks

* Using animation callbacks you can execute a method when an animation starts or is done
* `(@divState.start)="animationStarted()"` this method will get executed when the animation starts
* `(@divState.done)="animationDone()"` this method will get executed when the animation starts

## Section 24: Unit testing in angular

* Unit testing allows you to test specific elements of the Angular app (components, pipes, services)
* Analyze code behavior for expected and unexpected behavior
* `import { TestBed, async } from '@angular/core/testing';` testing package
* This code is ran before each individual test:
```
beforeEach(() => {
  TestBed.configureTestingModule({
    declarations: [
      AppComponent
    ],
  });
});
```
This is which code you want to have in each testing environment:
```
it('should create the app', async(() => {
  let fixture = TestBed.createComponent(AppComponent);
  let app = fixture.debugElement.componentInstance;
  expect(app).toBeTruthy();
}));
```
* `fixture` holds the component you create in the Testbed
* `it` should create the app and then we `expect` something when it is done, like the app exists

* You can use testing packages like `jasmine`
* with the cli you can use `ng test` to start up the testing environments

### Isolated vs non isolated testing

* You can test things isolated, like a pipe. Then you test it by itself and independant of Angular

### More on testing

* https://angular.io/docs/ts/latest/guide/testing.html
* https://semaphoreci.com/community/tutorials/testing-components-in-angular-2-with-jasmine
* https://github.com/angular/angular-cli#running-unit-tests
* https://github.com/angular/angular-cli#running-end-to-end-tests

## Section 28: Typescript

* Typescript is a Javascript superset
* You can assign types to variables and properties, this reduces your chance to make errors by assigning the wrong types for example
* You can create classes, use interfaces, generic types and modules

### Types

* types is the core of Typescript
* If you assign a string to a variable it will automatically refer a type

```
let myString: string;

myString = 'This is a string'; // This is ok
myString = 7; // This gives an error
```
* Basic types:
```
let aString: string;
let aNumber: number;
let aBoolean: boolean;
let anArray: Array<string>; // This is a generic type => May only hold 'strings' in this case
let anything: any; // Any can be used if we don't know the actual type => Use it rarely!
// We also got void (=> nothing) and enums (a set of numeric values)
```

### Classes

```
// How to create a class

class Car {
    engineName: string;
    gears: number;
    private speed: number; // private properties can't be accessed from outside the class

    constructor(speed: number) {
        this.speed = speed || 0;
    }

    accelerate(): void {
        this.speed++;
    }

    throttle():void {
        this.speed--;
    }

    getSpeed():void {
        console.log(this.speed);
    }

    static numberOfWheels(): number {
        return 4;
    }
}

// Instantiate (create) an object from a class

let car = new Car(5);
car.accelerate();
car.getSpeed();

console.log(Car.numberOfWheels());
```

### Interfaces

* An Interface is like a contract (whatever implements this interace, must have these properties)
* Interfaces allow us to create a secure form of communication between objects

### Generics

```
let numberArray: Array<number>; // This array will only accept numbers

// Try to initialize it with strings

// numberArray = ['test']; // => Error
numberArray = [1,2,3];
```

### Modules

* With modules you can tell Typescript that a certain class can be used outside of it's own file, inside other files

```
export class ExportedClass {
    // This class is exported
}
```

### More on Typescript

*  http://www.typescriptlang.org/Handbook
* https://www.udemy.com/typescript/
