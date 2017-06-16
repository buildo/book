# Step 3

You have probably noticed that our component has a bug: it says "Good morning" at any time of the day. This is a good example of a small amount of logic you often need in your UI components.

To maintain things tidy and easy to test, [react-skinnable](https://github.com/buildo/react-skinnable) provides the `@skinnable` decorator. Let's import it and add it to our component:

```js
import skinnable from 'react-skinnable';
```

```js
@skinnable()
@props({
  formal: t.Boolean,
  toggle: t.Function
})
export default class Hello extends React.PureComponent {
```

The new decorator requires your component to implement two methods:

1. `template()`, which will replace your `render()` method, and receive an object containing the properties it needs

```js
template({ greeting, toggle }) {
  return (
    <div className='hello'>
      <h1>
        <a onClick={toggle}>{greeting}</a>
      </h1>
    </div>
  );
}
```

2. `getLocals()`, which will contain the logic and return the object expected by the `template()` method above

```js
getLocals({ formal, toggle }) {
  const greeting = formal ? formalGreeting() : 'Hello';

  return { greeting, toggle };
}
```

Finally, let's implement a naive way to generate the correct greeting (you should define this outside the component, since there is no reason to put it inside it):

```js
function formalGreeting() {
  const hours = new Date().getHours();
  if (hours > 20) {
    return 'Good Night';
  } else if (hours > 13) {
    return 'Good Afternoon';
  } else {
    return 'Good Morning';
  }
}
```

## Testing getLocals()

One big win of using this approach is that it is now trivial to test the behaviour of this component without rendering DOM elements:

```js
const props = { formal: false, toggle: () => {} };
const instance = new Hello(props);
const { greeting } = instance.getLocals(props);
expect(greeting).toBe("Hello");
```

Despite this, it is not something we do it often in practite. But it's still good to know.

## Step2 -> Step3 diff

You can check the `Step 3` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
