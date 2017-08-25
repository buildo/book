# Step 3

You have probably noticed that our component has a bug: it says "Good morning" at any time of the day. This is a good example of a small amount of logic you often need in your UI components, and that you don't want to put in the container since it does not rely on the app state or on some external props.

Let's implement a naive way to generate the correct greeting (you should define this outside the component, since there is no reason to put it inside it):

```ts
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

and let's use it in the render method as follows:

```tsx
render() {
  const { formal, toggle } = this.props;
  const greeting = formal ? formalGreeting() : 'Hello';

  return (
    <div className='hello'>
      <h1>
        <a onClick={toggle}>{greeting}</a>
      </h1>
    </div>
  );
}
```

Notice how we extracted the references to `this.props` from the render method: it is a good practice to separate the UI and the internal logic of the component,
so that the render method is as clean as possible and the JSX only references previously defined constants.

## Step2 -> Step3 diff

You can check the `Step 3` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
