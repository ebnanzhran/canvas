# Hooks API Reference

## Basic Hooks
### useState
```
const [state, setState] = useState(initialState);
```
Returns a stateful value, and a function to update it.

During the initial render, the returned state (state) is the same as the value passed as the first argument (initialState).

The setState function is used to update the state. It accepts a new state value and enqueues a re-render of the component.
```
setState(newState);
```
During subsequent re-renders, the first value returned by useState will always be the most recent state after applying updates.

Functional updates
If the new state is computed using the previous state, you can pass a function to setState. The function will receive the previous value, and return an updated value. Here’s an example of a counter component that uses both forms of setState:

```
function Counter({initialCount}) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
    </>
  );
}
```
The ”+” and ”-” buttons use the functional form, because the updated value is based on the previous value. But the “Reset” button uses the normal form, because it always sets the count back to the initial value.

If your update function returns the exact same value as the current state, the subsequent rerender will be skipped completely.


### Lazy initial state
The initialState argument is the state used during the initial render. In subsequent renders, it is disregarded. If the initial state is the result of an expensive computation, you may provide a function instead, which will be executed only on the initial render:
```
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});

```
### useEffect
```
useEffect(didUpdate);
```
Accepts a function that contains imperative, possibly effectful code.

Mutations, subscriptions, timers, logging, and other side effects are not allowed inside the main body of a function component (referred to as React’s render phase). Doing so will lead to confusing bugs and inconsistencies in the UI.

Instead, use useEffect. The function passed to useEffect will run after the render is committed to the screen. Think of effects as an escape hatch from React’s purely functional world into the imperative world.

By default, effects run after every completed render, but you can choose to fire them only when certain values have changed.

### Cleaning up an effect
Often, effects create resources that need to be cleaned up before the component leaves the screen, such as a subscription or timer ID. To do this, the function passed to useEffect may return a clean-up function. For example, to create a subscription:
```
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Clean up the subscription
    subscription.unsubscribe();
  };
});
```
The clean-up function runs before the component is removed from the UI to prevent memory leaks. Additionally, if a component renders multiple times (as they typically do), the previous effect is cleaned up before executing the next effect. In our example, this means a new subscription is created on every update. To avoid firing an effect on every update, refer to the next section.

To implement this, pass a second argument to useEffect that is the array of values that the effect depends on. Our updated example now looks like this:
```
useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);
```