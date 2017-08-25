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
  run: Promise.resolve.bind(Promise)
});
```

The name and the `id` property value should always be the same, and they are the name you will use to refer to this command in the rest of your app.

`invalidates` lists the _Queries_ that need to be refreshed when this command is executed.

`run` lets you specify a Promise that can for example send a _POST_ to your API. In this case, for a simple refresh command, invalidating the query is enough and we can use `::Promise.resolve` providing a Promise that will resolve immediately. In case you want to define a command that performs an API call (e.g., a `POST`) you should define it in the `src/app/API.js` file, like we did for the query in the previous step, and call it in the `run` property of your `Command`.

## Bind it to your container

By this time you should have guessed that the way to bind your new `Command` to your existing `Hello` component is through `HelloContainer`, using more `container` magic.

Specify an array of `commands` you want to be accessible from the props of your component, and don't forget to add `doRefreshUser: () => Promise<void>` to the `MapProps` type:

```ts
export default container(noLoaderLoading(Hello))({
  connect: ['formal'],
  queries: ['user'],
  commands: ['doRefreshUser'],
  mapProps: ({ transition, formal = false, user, doRefreshUser }: MapProps) => ({
    toggle: () => {
      transition({ formal: !formal });
    },
    formal,
    user,
    onRefreshClick: () => doRefreshUser()
  })
}) as any as React.ComponentType;
```

## Updating the UI component

The container is now providing an `onRefreshClick` function that is ready to be used in `Hello.tsx`. Start by adding it to the `Props` type:

```ts
onRefreshClick: () => Promise<void>
```

Then extract it from `this.props` in the `render` method:

```ts
const { formal, toggle, user, onRefreshClick } = this.props;
```

and render it by adding the following after the `h1` closing tag:

```tsx
<a onClick={onRefreshClick}>(refresh)</a>
```

## Step4 -> Step5 diff

You can check the `Step 5` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
