# Step 5

What if you want to trigger a change based on a UI action? The most common scenarios are a user clicking a button, or submitting a form. This is where you need Avenger `Commands`.

## Your first Command

Let's implement a simple "refresh" command in the `src/app/commands.js` file.

```js
import { Command } from 'avenger/lib/graph';
import queries from 'queries';

export const doRefreshUser = Command({
  id: 'doRefreshUser',
  invalidates: { user: queries.user },
  run: ::Promise.resolve
});
```

The name and the `id` property value should always be the same, and they are the name you will use to refer to this command in the rest of your app.

`invalidates` lists the _Queries_ that need to be refreshed when this command is executed.

`run` lets you specify a Promise that can for example send a _POST_ to your API. In this case, for a simple refresh command, invalidating the query is enough and we can use `::Promise.resolve` providing a Promise that will resolve immediately. In case you want to define a command that performs an API call (e.g., a `POST`) you should define it in the `src/app/API.js` file, like we did for the query in the previous step, and call it in the `run` property of your `Command`.

## Bind it to your container

By this time you should have guessed that the way to bind your new `Command` to your existing `Hello` component is through `HelloContainer`, using more `container` magic.

Specify an array of `commands` you want to be accessible from the props of your component

```js
export default container(Hello, {
  connect: { formal: t.maybe(t.Boolean) },
  queries: ['user'],
  commands: ['doRefreshUser'],
  mapProps: ({ transition, formal = false, user, doRefreshUser }) => ({
    toggle: () => {
      transition({ formal: !formal });
    },
    formal,
    user,
    onRefreshClick: () => doRefreshUser()
  })
});
```

## Updating the UI component

The container is now providing an `onRefreshClick` function that is ready to be used in `Hello.js`. Start by adding it to the `@props` object:

```js
onRefreshClick: t.Function
```

Then update `getLocals()`:

```js
getLocals({ formal, toggle, user, onRefreshClick }) {
  const greeting = formal ? formalGreeting() : 'Hello';

  return { greeting, toggle, user, onRefreshClick };
}
```

And finally your template:

```js
template({ greeting, toggle, user, onRefreshClick }) {
  return (
    <div className='hello'>
      <h1>
        <a onClick={toggle}>{greeting}</a> {user}
      </h1>
      <a onClick={onRefreshClick}>(refresh)</a>
    </div>
  );
}
```

## Step4 -> Step5 diff

You can check the `Step 5` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
