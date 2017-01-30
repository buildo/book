# Step 5

What if you want to trigger a change based on a UI action? The most common scenarios are a user clicking a button, or submitting a form. This is where you need Avenger `Commands`.

## Your first Command

Let's implement a simple "refresh" command.

```js
import { Command } from 'avenger';
import queries from 'queries';

const commands = {

  doRefreshUser: Command({
    id: 'doRefreshUser',
    invalidates: { user: queries.user },
    run: ::Promise.resolve
  })

};
```

The property name and the `id` should always be the same, and they are the name you will use to refer to this command in the rest of your app.

`invalidates` lists the _Queries_ that need to be refreshed when this command is executed.

`run` lets you specify a Promise that can for example send a _POST_ to your API. In this case, for a simple refresh command, invalidating the query is enough and we can use `::Promise.resolve` providing a Promise that will resolve immediately. We will see an example of using `run` later in the tutorial.

## Bind it to your container

By this time you should have guessed the way to bind your new `Command` to your existing `Hello` component is through `HelloContainer`, using more `react-container` magic.

Add a new `allCommands` property when initializing your container:

```js
import allCommands from 'commands';
const container = containerFactory({ allQueries, allCommands });
```

Then when instantiating `HelloContainer`, specify an array of `commands` you want to be accessible from the props of your component

```js
  commands: ['doRefreshUser'],
  mapProps: ({ transition, formal = false, user, doRefreshUser }) => ({
    ...
    onRefreshClick: () => doRefreshUser()
```

## Updating the UI component

The container is now providing an `onRefreshClick` function that is ready to be used in `Hello.js`. Start by adding it to the `@props` object:

```js
onRefreshClick: t.Function
```

Then update `getLocals()`:

```js
getLocals({ toggle, user, onRefreshClick, formal }) {
  const greeting = formal ? this.formalGreeting() : 'Hello';

  return { toggle, greeting, user, onRefreshClick };
}
```

And finally drop an anchor somewhere in your template:

```js
<a onClick={onRefreshClick}>(refresh)</a>
```

## Step4->Step5

Check the [full diff](https://github.com/buildo/webseed/compare/tutorial-step4...tutorial-step5) between Step 4 and Step 5.
