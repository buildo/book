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

Then define your first `avenger` Query in `src/app/queries.js`:

```javascript
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

In `HelloContainer.js` you can now ask the `container` to bind our `Hello` component to the *Avenger* query you have just created.

Invoke `container()` as before, with an additional `queries: ['user']` property. This will add a new `user` property to the input of `mapProps()`.

```js
export default container(Hello, {
  connect: { formal: t.maybe(t.Boolean) },
  queries: ['user'],
  mapProps: ({ transition, formal = false, user }) => ({
    toggle: () => {
      transition({ formal: !formal });
    },
    formal,
    user
  })
});
```

## Updating the UI component

Back in `Hello.js` you just need to reference the new `user` prop.

Start by adding it to the `@props` list:

```js
@props({
  formal: t.Boolean,
  toggle: t.Function,
  user: t.String
})
```

Then make sure `getLocals()` is forwarding it to the `template()` function:

```js
getLocals({ formal, toggle, user }) {
  const greeting = formal ? formalGreeting() : 'Hello';

  return { greeting, toggle, user };
}
```

And finally render it!

```js
template({ greeting, toggle, user }) {
  return (
    <div className='hello'>
      <h1>
        <a onClick={toggle}>{greeting}</a> {user}
      </h1>
    </div>
  );
}
```

## What to do when waiting for the query data

In this step, we can simply decide to not handle the loading situation (i.e., not notify the user about the fact that we are waiting for the `user` query result).

In the `Hello.js` add the following import:

```js
import { noLoaderLoading } from 'react-avenger/lib/loading';
```

And the following decorator:

```js
@noLoaderLoading
```

## Step3 -> Step4 diff

You can check the `Step 4` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
