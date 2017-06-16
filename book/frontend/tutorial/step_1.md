# Step 1

Now it's time to start writing some code. Fire up ~~Vim~~ your favorite editor and open `src/app/components/Hello/Hello.js`.

## Make the component dynamic

This is so far a very basic static React component. Let's make it a bit nicer and support a more formal greeting:

```js
<h1>
  <a onClick={this.toggle}>{this.props.formal ? 'Good Morning' : 'Hello'}</a>
</h1>
```

When `formal` is set to true, the component will switch from displaying 'Hello' to displaying 'Good Morning'. If we click on it, we want the component to toggle between the formal and informal greetings.

## Global state

We don't want to store the current state (formal or informal) in `this.state`. Instead we will store it in a global state object, akin to the `store` in Redux or the global atom in Om.

To do this, we use a small library called [buildo-state](https://github.com/buildo/state), and we also validate types using [tcomb](https://github.com/gcanti/tcomb). Let's add both to our imports:

```js
import { props, t } from 'tcomb-react';
import connect from 'buildo-state/lib/connect';
```

Now we are ready to add a couple more decorators to our component:

```js
@connect({ formal: t.maybe(t.Boolean) })
@props({
  transition: t.Function,
  formal: t.maybe(t.Boolean)
})
```

`@connect`, as the name suggests, connects our component with some properties in our global state. In this case, we're interested in a single property from the global state called `formal`.

`@connect` injects two new `props` into our component:
 * `formal`, containing the current value of that property in the global state
 * `transition()`, a function we can use to request an update to the global state.

One thing that is worth mentioning is that the global state, in this way, is defined locally: there isn't a centralized module where all the state variables should be declared. You can still connect to `formal` from another component without any problem: it will just look for its value in the state and you don't have to worry about it.

## Let's write our handler function

Finally, let's create the click handler, which will use `transition()` to signal it wants to update the global state with a new value for `formal`:

```js
toggle = () => {
  this.props.transition({
    formal: !this.props.formal
  });
}
 ```
## Step0 -> Step1 diff

If you want to see how your `Hello.js` component looks after all these changes, check the `Step 1` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
