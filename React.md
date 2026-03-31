````markdown
# jsx, props, state, event listeners

## How react rendering works and why it is so fast?

React Internals: JSX, Virtual DOM, and Reconciliation

1. JSX and JavaScript Objects
   The Blueprint: React elements are plain JavaScript objects.

The Compilation: Compilers like Babel or SWC parse JSX. In modern React (17+), they convert JSX into special functions (e.g., \_jsx) that return these UI objects.

The Creation: You can observe these objects by looking at the output of React.createElement('div', { props }, children).

The Tree: React maintains a tree of these objects known as the Virtual DOM.

2. The Update Cycle (Render & Commit)
   When a state variable changes, React doesn't immediately touch the browser. It goes through two distinct phases:

Phase A: The Render Phase (Reconciliation)

New Tree: React creates a new Virtual DOM tree based on the updated state.

The Diffing: React compares the Old Virtual DOM with the New Virtual DOM.

React Fiber: This is the internal engine that manages this comparison. It’s "incremental," meaning it can pause heavy work to keep the browser responsive.

The Strategy: React uses a "Heuristic Diffing Algorithm" to find the minimum number of changes needed.

Key Optimization: If a node has a unique key, React can track it across renders instead of re-creating it.

Phase B: The Commit Phase

DOM Manipulation: Once the differences are calculated, React (via react-dom) applies only those specific changes to the real browser DOM.

Efficiency: If only one word in a paragraph changes, React only updates that text node, not the entire page.

3. Advanced Mechanics to Remember
   Automatic Batching: If you update multiple state variables at once, React "batches" them. It performs one single Reconciliation/Commit cycle for all updates to maximize performance.

Immutability: React relies on state being "immutable." It checks if the reference of the state object has changed. If you mutate an object directly (e.g., myState.name = 'New'), React might not realize a change happened and won't trigger a re-render.

## state :

when you want UI to be updated based on some variable , that variable should be stored as a state variable.

example :

```javascript
const [stateVar, setStateVar] = useState(initialValue);
```
````

`useState(initialValue)` do two things

1. initialize state variable with it's initial value and
2. returns pair of that variable reference and the function that will be used to update the state.

so now when you want to update the state value , you should call `setStateVar(newValue or function that returns new value)`. It tells react to update the UI because the state variable has changed.

when you want to update state based on the previous state, you have two way to do that :

suppose you want to increment the counter var based on button click.

```javascript
onClickHandle() {
  setCounter(counter+1);
  // OR
  setCounter( (prevCounter) => prevCounter + 1);
}

```

when you pass a function in `setState()` function that callback function automatically get the prevStateValue in it's argument. so when you want to update the state 2 or more times in same function like below then using the first approach you won't get previous state value because you are calling the `setState()` function with the same value.

```javascript
counter = 2;
onClickHandle() {
  setCounter(counter+1); // 2+1
  setCounter(counter+2); // 2+1
}

```

so you won't get expected result. but using the callback function appraoch you will get the prevState value as a argument so you can update the stateVAlue based on the prevValue.

```javascript
onClickHandle() {
  setCounter((prevCounter)=>prevCounter + 1); // set counter state variable to 3
  setCounter((prevCounter)=>prevCounter + 1); // and it will receive 3 as argument and setCounter to 4
}

```

---

## Styling in React :

1. style prop like `style={{color:'red',textAlign:'center',backgroundColor: someCondition ? 'green' : undefined}}`
2. ClassName like `className={classAbc}`

styles in react are not scoped by default.

you can scope styles in react in below ways.

1. **css modules** => add `.module` in css file names and the build tool like vite will generate scoped style rules for you. example css fileName = `abc.module.css`
   you have to import this css files like `import classes from 'abc.module.css'` and then you can use classes defined inside that css file like `classes.className`
2. **styled components** =>

---

## useRef :

`useRef` hook in react allows you to bind an javascript variable to which stores reference of an html element.

```javascript
const inputRef = useRef(); // this way you can createReference variable and bind that to input element using following way
```

```jsx
<input ref={inputRef} />
```

when the value of ref element changes component won't get rerendered like it get in state changes

we can also use Refs to hold a value that needs to persist after the component gets rerendered but , on change of that value component should not get rerendered.
In older react versions you have to use `forwardRef` function to wrap the component to which we are supposed to forward the reference.

---

## useImperativeHandle :

this hook is help us to expose any function or property to other components.
It's been used when ref is forwarded to the component that wants to expose the functions or properties. It takes two arguments first is ref variable and the second one is the callback function which returns the object that has the functions and properties you want to expose.
