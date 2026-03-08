```markdown
* **pull mechanism** : function calls or iterators because we need to call function to generate values when we need values
* **push mechanism** : promises and observables , they produce values by themselves 

## Observables 
: are producers of values

* they are lazy because we have to subscribe to execute the callback. unlike events are eager which automatically triggers the callback when event occurs.
* subscription of observables are syncrhonous but observables can emit values syncrhonously or asynchronously
* they can be created mannually using constructor like below or with an creater operators like `of`, `from` , `interval` etc.
* `new Observable()` costructor takes one argument which is subscribe function. subscribe function takes one argument with observer objects which holds callback values like `next`, `error`, `complete` etc.
* when you subscribe observable the subscribe function will get called.
	
## Subjects 
: subjects are observable which can multicast the values. It's like an observables which does not create new execution when get subscribed but adds that observer in it's registry so that in future it will also emit value to that observer.



* subjects are also observers with functions of each notifications , `next()`, `error()`, `complete()`. you can provide it while subscribing to the plain observale
* **behaviour subject** holds the current value so that it will emit that value when new observer subscribe that subject.
* **replay subject** : it's similar to behaviour subject , but it takes argument let say 3 so it holds 3 values and delivers to the observer when observer subcribes that subject : you can also provide window time to specify how old the value can be
* **async subject** : multicast the last value to the observer when it completes.

## operators : 

All below operators comes in handy when the operator emits new observable. so it becomes hire order observables.


	
* `concatAll()` : subscribe to inner observable : completes it : subscribe to next inner observable
* `mergeAll()` : subscribe to all inner observable parellelly
* `swithcAll()` : subscribe to first inner observable and if meanwhile comes new variable it cancels previous one and subscribes to new one
* `exhuastAll()` : subscribe to first inner observable and ignore all until the first one completes

```