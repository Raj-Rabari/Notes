# signals

**signals** : It's wrapper around value that notifies angular when the value is changed.

**writable signal** : you can create writablesignal like 
```typescript
val1: WritableSignal<number> = signal(1);
val1.set(2) or val1.update(a => a*2) // update operation

**computed signal** : you can create computed signal like below.

val2 = computed<number>(() => val1() * 2);

**benefits** : it's lazily evaluated means it does not evaluate it's value until you read it and it also cache the value so re-calculate only when the one of the source signal changes. so you can create values which needs heavy calculation.