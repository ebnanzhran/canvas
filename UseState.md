# Use State()

## Introducing Hooks
Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

```
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
This new function useState is the first “Hook” we’ll learn about, but this example is just a teaser. Don’t worry if it doesn’t make sense yet!

## No Breaking Changes
Before we continue, note that Hooks are:

* Completely opt-in. You can try Hooks in a few components without rewriting any existing code. But you don’t have to learn or use Hooks right now if you don’t want to.
* 100% backwards-compatible. Hooks don’t contain any breaking changes.
* Available now. Hooks are now available with the release of v16.8.0.

## Motivation
Hooks solve a wide variety of seemingly unconnected problems in React that we’ve encountered over five years of writing and maintaining tens of thousands of components. Whether you’re learning React, use it daily, or even prefer a different library with a similar component model, you might recognize some of these problems.


Equivalent Class Example
If you used classes in React before, this code should look familiar:
```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}

```
The state starts as { count: 0 }, and we increment state.count when the user clicks a button by calling this.setState(). We’ll use snippets from this class throughout the page.

Hooks and Function Components
As a reminder, function components in React look like this:
```
const Example = (props) => {
  // You can use Hooks here!
  return <div />;
}
```

or this:
```
function Example(props) {
  // You can use Hooks here!
  return <div />;
}
```
You might have previously known these as “stateless components”. We’re now introducing the ability to use React state from these, so we prefer the name “function components”.