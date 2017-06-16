# Step 2

Adding things like `@connect` and `transition()` to our UI components is not ideal: they become tightly coupled to our libraries and harder to reuse.

To avoid this, we usually separate our components into two files: a stateless UI React component and a **container**.

## Our first container

Let's create a new file called `HelloContainer.js` next to our existing `Hello.js`:

```js
import t from 'tcomb';
import container from 'container';
import Hello from './Hello';

export default container(Hello, {
  connect: { formal: t.maybe(t.Boolean) },
  mapProps: ({ transition, formal = false }) => ({
    toggle: () => {
      transition({ formal: !formal });
    },
    formal
  })
});
```

There is some magic here, but the important thing to note is we use the `container()` helper to wrap our `Hello` component, providing a `mapProps()` function. The input of this function is a rich set of properties, including the `transition()` function we discussed in the previous step. The output is a minimal set of stateless properties that are required by the UI component.

## Back to Hello.js

We can now simplify our UI component to this:
```js
@intlMethods
@props({
  formal: t.Boolean,
  toggle: t.Function
})
export default class Hello extends React.PureComponent {

  render() {
    return (
      <div className='hello'>
        <h1>
          <a onClick={this.props.toggle}>{this.props.formal ? 'Good Morning' : 'Hello'}</a>
        </h1>
      </div>
    );
  }

}
```

Notice how we removed any reference to `@connect` or `transition()`. Also, the component is now _really_ stateless as it doesn't handle the `onClick` event anymore. Instead, it just delegates to whatever function it receives in `props.toggle`.

Another bonus point: we have removed the `t.maybe` type. It's the responsibility of the _container_ to make sure `formal` and `toggle` are always defined and of the correct type.

## Checking it all works

Modify the `index.js` file in the same folder to make it export the container instead of the component itself:

```js
export default from './HelloContainer';
```

Hopefully, your component should work exactly as before!

## Step1 -> Step2 diff

As with the previous step, you can check the `Step 2` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).

