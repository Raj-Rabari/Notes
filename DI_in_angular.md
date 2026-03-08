# DI in angular

Angular provides dependency injection concept to share common business logic and data among it's components, directives , or any other part of the application.
Dependency could be anything, instance of any class or any static value.

Class instances are most commonly used as dependency in angular.
We can create any class with decorator `@Injectable()` decorator, to use it as an dependency in our application.

suppose we can create any service class to share any user specific data and methods to handle  that data.

There are two main things in this concept.

1. **dependency providers** => as name suggests , it provides the dependency
2. **dependency consumers** => same => it consumes dependency.

---

## 1. dependency consumers 
=> you can consume any dependency, by injecting it via constructor or via `inject()` function.

## 2. dependency providers 
=> When any consumer tries to consume any dependency, angular checks who provides this dependency.

you can provide any dependency In following ways.

Before you dive into dependency providers , understand injector.

**Injector** => you can think it as a registry where angular checks for dependency.

1. **using environmental injector** => by defining property in `@Injectable()` decorator => `providedIn : 'root'` or `'any'` or `'platform'` 
Or in providers array of appConfig
2. **Using element injector** => in providers array of any component, directives or module.

* `providedIn: 'root'` => creates application wide injector.
* `providedIn: 'any'` => creates one instance for eagarly loaded modules and another instances for other lazy loaded modules.
* `providedIn: 'platform'` => creates platform (Browser) wide instance to share the business logic between multi application running on same platform.

When you provide any dependency in Element Injector ( like in providers array of any component, module or directives ) , It will create new instance for that element and it's childs.

---

## * How angular resolves the dependency : 
=> When angular finds any consumer, it starts resolving dependency in following way.

* It looks for the dependency in Element Injector heirarchy => like in Element's own injector => it's parent element injector => and show on.
* If it doesn't find it in Element injector heirarchy then it checks in Environmental Injectors. => like whether it's provided in application level ('root') or in platform
* For NgModule based application, there are one more ModuleLevel injector which angular looks for.

=> if it doesn't find dependency in any of above Injector then it gives NullInjector error.

---

## * We can modify Angular dependency resolving flow by using resolution modifiers.

* `@Optional` => It doesn't throw NullInjector error if it doesn't find dependency provider , while resolving dependency using heirarchy Injectors.
* `@self` => It only checks in Element's own injector, if it doesn't find it there, throws NullInjector Error.
* `@skipSelf` => It starts checking for dependency by skipping self and start from parent injector.
* `@Host` => It only checks in host element. if it doens't find it throws NullInjector error.

---

## Providing different types of dependency: 
structure of provider object.
`{ provide : injecton token, useClass/useExisting/useFactory/useValue }`
 
mostly we provide class based dependencies like below
`providers: [ UserService ]` , which is shorthand syntax of `{ provide: UserService, useClass: UserService }` 
Mostly we do have same class name and provider token name, so we use shorthand syntax mentioned above.

* **useExisting**: uses Existing dependency to providing new dependencies. It's basically aliasing the existing dependency.
* **useFactory**: We can provide function , that returns dependency instance based on some logic
* **useValue**: to provide static value.