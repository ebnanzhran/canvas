# Context API - Behaviors

## Necessity for the Design System
After performing an audit on how we communicate with our users, we landed with a simple system of three classes of communication, and snackbars fit perfectly on the ‘low priority’ end of that spectrum. They are small notifications that show up on the screen when a user performs an action. They are not intrusive at all and appear for just a brief moment.

## Dream State
From an engineering standpoint, our snackbar system must easy to use and generally be very lightweight. We want to be able to place one on the screen with just a couple of lines of code. Anything more and it’s overkill.

This means forget render props and higher order components. We don’t want to deal with a messy React tree and wrappers. We don’t want action creators, reducers*, or any of that stuff.

Hooks are a perfect fit here. So lets imagine we have a custom hook that lets us do this and work backwards.


## Globally Accessible
The state of our snackbars (which ones are visible) can be localized to a single centralized component. That same centralized component can be responsible for rendering them. There’s really no need for another component somewhere in the tree to hook into that state (at least not in our use-case).

However, the management of that state (adding, removing) needs to be globally accessible.

## Higher Level API & Behaviour

There’s a lot more happening now. Our provider now exposes a new function called addAlert. This function uses the local state mutator useState to properly append a new alert without destroying existing ones. You could do more fancy things here: de-dup alerts, assign unique IDs to alerts so that we can also expose a removeAlert function that makes use of those IDs, and so on. But we’re going to keep it simple.

Most importantly perhaps is that we now make use of useEffect to display each alert for 5 seconds on the screen.

When a new alert is added, the component is re-rendered, and the effect is executed. In that effect, a timer is kicked off to remove the oldest living alert after a delay. This timer is a side-effect of that render.

When an alert is removed as a result of the above timer expiring, this component is re-rendered with the new state of alerts. Just as before, the side-effect will run, creating a new timer. Before doing that though, it will clean up the side-effect from the previous render (by clearing the timer). The timer is essentially restarted (by deleting the old timer and creating a new one).

This render and side-effect process repeats until alerts /activeAlertIds is empty. This is our base case if you want to think of this recursively.

## Sprinkling in Optimizations
Our custom hook is now fully operational! We can add alerts easily from anywhere and our provider will display them for us. We could stop here, but there’s room for some optimizations that are pretty easy to achieve.

You’ll notice that value is a new object being created every single time this provider is rendered. That’s not great, because anything consuming this value from the context will potentially also be getting re-rendered.

We can use useMemo to memoize value . There’s no reason this object needs to be re-created every time. We’ll pass to it addAlert as a dependency, i.e. the memoization cache needs to be re-filled if addAlert changes.

# Awesome React Context

## Libraries

* react-create-context - Polyfill for the proposed React context API.
* react-contextual - Tiny helper around React's new context API.
* react-broadcast - Reliably communicate state changes to deeply nested React elements.
* react-composer - Prevents deeply nested code when consuming multiple contexts at the same time.
* react-connect-context - Redux-style connector that maps context-based objects onto a component's props.
* react-waterfall - React store built on top of the new context API.
* react-redux - A Context based library for integrating React with Redux.
* react-zedux - Create consumable contexts from observables, including Zedux/Redux stores.
* react-translations-provider - Setup and access a global set of translations and current locale via a context provider.