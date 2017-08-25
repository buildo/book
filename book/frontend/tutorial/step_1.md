# Step 1

Now it's time to start writing some code. Fire up ~~Vim~~ your favorite editor and open `src/app/components/Hello/Hello.tsx`.

## Make the component dynamic

This is so far a very basic static React component. Let's make it a bit nicer and support a more formal greeting:

```tsx
<h1>
  <a onClick={this.toggle}>{this.props.formal ? 'Good Morning' : 'Hello'}</a>
</h1>
```

When `formal` is set to true, the component will switch from displaying 'Hello' to displaying 'Good Morning'. If we click on it, we want the component to toggle between the formal and informal greetings.

## Global state

We don't want to store the current state (formal or informal) in `this.state`. Instead we will store it in a global state object, akin to the `store` in Redux or the global atom in Om.

To do this, we use a small library called [buildo-state](https://github.com/buildo/state).

First, we need to add the property to the global state by adding it to the interfaces defined in `src/app/state/state.ts`:

```ts
export interface AppState {
  //...
  formal?: boolean // Add this line to the TypeScript interface
}

export const AppState = t.interface<AppState>({
  //...
  formal: t.maybe(t.Boolean) // ...and this line to the tcomb interface
}, { strict: true });
```


Then, let's add the following to the `Hello` component imports; `connect` will be used to connect to the global state, while `TransitionFunction` is a type that we will use in the `Props` type definition:

```ts
import { TransitionFunction, connect as _connect } from 'state';
```

Now we are ready to define the type for the `Props` object that the componenet receives. To specify that TypeScript should use the `Props` type that we define to check the
type of the props, we need to add `<Props>` after the `React.PureComponent`:

```ts
const connect = _connect(['formal']);

type Props = {
  transition: TransitionFunction,
  formal?: boolean
};

class Hello extends React.PureComponent<Props> {
  //...
}

export default connect(Hello);
```

`connect`, as the name suggests, connects our component with some properties in our global state. In this case, we're interested in a single property from the global state called `formal`.

`connect` injects two new `props` into our component:
 * `formal`, containing the current value of that property in the global state
 * `transition`, a function we can use to request an update to the global state.

You can still connect to `formal` from another component without any problem: it will just look for its value in the state and you don't have to worry about it.

## Let's write our handler function

Finally, let's create the click handler, which will use `transition` to signal it wants to update the global state with a new value for `formal`:

```ts
toggle = () => {
  this.props.transition({
    formal: !this.props.formal
  });
}
 ```
## Step0 -> Step1 diff

If you want to see how your `Hello.tsx` component looks after all these changes, check the `Step 1` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
