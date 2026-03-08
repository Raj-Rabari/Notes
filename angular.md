
```markdown
# About bootstrapApplication() function.

* In `NgModule` `imports` array is for standalone components and `declarations` array is for non-standalone components.
* **viewEncapsulation.emulated** : only specific to elements directly within the component’s view.
* **viewEncapsulation.None** : component’s styles become global and added to head of the document to available throught the app.
* **viewEncapsulation.shadowDom** : global styles are first added to the host of the shadowDom and then component’s styles are added.



---

## Host element : 
for component named appOne, you can see the element in dom `app-one`. That element is component’s host element. And for directives host element is on which directives is applied.

If you want to bind any property to host element. Instead of binding it to every occurrence of it in templates of application. You can bind it using `@HostBinding()` decorator as below :
 
```typescript
@HostBinding('class') className = 'control';

```

Alternative and modern way of hostbinding decorator is you can set `host: {}` object in `@Component` decorator of component as below :

```typescript
host : {
  class : 'control'
}

```

For host listner :

```typescript
@HostListener('click') onClick () { }  // in component class

// Or 

host : {
  '(click)':'onClick()'
} // in component’s decorator

```

---

## Class binding sysntaxes :

Refere D:/code Practice/angular/secion 6

```html
[class.demoClass] = "{condition}"
[class] = " { demoClass2 : condition, demoClass3 : condition } "

```

---

## Style bindings :

both dash and camel case names of properties will work. (refer section 6 angular course )

```typescript
[style] = {
  fontSize : '34px',
  'font-size' : currentSTatus === online ? '34px' : '45px'
}

```

```
                OR 

```

```typescript
[style.fontSize] = "'34px'"

```

---

* You can use `@ViewChild()` or `viewChild()` [new feature angular 17.3 or later)  to get an reference of any element in component’s view. Both accepts component class or template reference variable
* Same as above for the `@ViewContent()` and `viewContent()`

---

## Effects in signal :

Angular by default subscribe to the signal wherever it gets read in template and updates the value when it changes. But when you need to run some code when signal’s value is get changed you have to use effect. Effect accepts callback function and that callback function gets executed every time when any of signal value referenced inside that callback function changes.

---

## Directives :

it’s component’s without template. There are two types of directives attribute directives which exhances the behaviour of the host element and the structural directives which adds or removes the host elements from the dom.
Structural directives are written with `*`. `*` Behind the scene wraps the content in `ng-template`.
Content inside `ng-template` does not shown on the dom initially but it will be rendered conditionally.

---

## angular change detection:

* by default angular rely on zone.js for change detection. whenever any timer expires or any event occurs in any component angular change detection runs for all the components from root to leave.
* In angular OnPush change detection strategy , angular runs change detection for that component only if any event ( timers or any other event) occurs or inputs changes for  that component or it's child components.
* In angular 18 , you can use experimentalZoneless change detection strategy with signals. so whenever any signal value changes in component. change detection runs for that component.

---

## Template Driven form :

* add `ngModel` to the form input without two way binding syntax
* add temlpate reference variable to the form element with initial value `ngForm`
* now you can get an angular form object set in that template reference variable

---

## routing :

* by calling `withComponentInputBinding()` functions as argument of `providerRouter()` , It binds the route parameters to the component's input property and you can get it inside component using `input()` or `@Input`
* by calling `withComponentInputBinding()` inside `provideRouter()` function , you can bind any route property (like params,queryParams,data etc ) with input property of component
* if you want to get access to the params of the parent route , you can have it using activatedRoute or you have to call `withRouterConfig({paramsInheritanceStrategy: 'always'})` inside `providerRouter()` and in the argument object set `paramsInheritanceStrategy: 'always'`
* you can pass static data to the route using key value pair inside data property object
* but if you want to pass dynamic data which is depends on route parameters or queryParams the you can write a logic to get it inside resolver function and you have to assign that function inside resolve property object, resolve property object is same as data object but you have to pass resolver function as a value that can compute the value based on route parameters. It must have type of ResolveFn which accepts two parameter 1. activatedRoutesnapshot and 2. routerStateSnapshot
* by default resolver function executed when route parameter changes but you can control this behaviour by adding property runGuardAndResolvers to it's appropriate value like paramsOrQueryParamsChange
* now if you have binded input properties which depends on route parameters and provided it using resolve guard, then if it changes within the same component , resolve guard won't run because navigation is not occured. for that you have to navigate to current route using router.navigate method where you are expecting the input to be change and make that resolverGuard to run always using the property runGuardAndResolvers, By doing this you can route to the existing route but you loose the queryparams. To preserve it you have to add property inside config object of navigate method that : queryParams to preserve