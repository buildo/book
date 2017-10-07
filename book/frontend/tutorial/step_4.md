# Step 4

# Avenger

Most web applications need to frequently synchronize data with a server using HTTP calls.

To manage these calls in a simple and consistent manner, we created [Avenger](https://github.com/buildo/avenger). It's a powerful data-fetching library supporting batching, caching, data dependencies and much more.

The basic units of Avenger are *Queries* and *Commands*, following [CQRS](https://en.wikipedia.org/wiki/Command%E2%80%93query_separation#Command_Query_Responsibility_Segregation) principles. We will start by creating a *Query* and we will explore *Commands* in Step 5.

## Creating your first Query

Define your API call in `src/app/API.js` using promises:

```js
export const getUser = () => {
  return fetch('http://uinames.com/api/').then(res => res.json()).then(res => {
    return res.name;
  });
};
```

Then define your first `avenger` Query in `src/app/queries/queries.js`:

```js
import { Query } from 'avenger/lib/graph';
import { Expire } from 'avenger/lib/cache/strategies';
import t from 'tcomb';
import * as API from 'API';

export const user = Query({
  id: 'user',
  chacheStrategy: new Expire(2000),
  returnType: t.String,
  fetch: API.getUser
});
```

## More container magic

In `HelloContainer.ts` you can now ask the `container` to bind our `Hello` component to the *Avenger* query you have just created.

Invoke `container` as before, with an additional `queries: ['user']` property. This will add a new `user` property to the input of `mapProps` (remember also to add `user: string` to the `MapProps` type).

```ts
export default container(Hello)({
  connect: ['formal'],
  queries: ['user'],
  mapProps: ({ transition, formal = false, user }: MapProps) => ({
    toggle: () => {
      transition({ formal: !formal });
    },
    formal,
    user
  })
}) as any as React.ComponentType;
```

## Updating the UI component

Back in `Hello.tsx` you just need to reference the new `user` prop.

Start by adding it to the `Props` type:

```ts
 type Props = {
  //...
  user: string
};
```

Then extract it from `this.props` in the `render` method and render it:

```tsx
const { formal, toggle, user } = this.props;
```

```tsx
<a onClick={toggle}>{greeting}</a> {user}
```

## What to do when waiting for the query data

In this step, we can simply decide to not handle the loading situation (i.e., not notify the user about the fact that we are waiting for the `user` query result).

In the `HelloContainer.ts` add the following import:

```ts
import { noLoaderLoading } from 'react-avenger/lib/loading';
```

And pass `noLoaderLoading(Hello)` instead of just `Hello` to the `container`.

## Step3 -> Step4 diff

You can check the `Step 4` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
