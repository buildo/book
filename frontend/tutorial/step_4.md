# Step 4

# Avenger

Most web applications need to frequently synchronize data with a server using HTTP calls.

To manage these calls in a simple and consistent manner, we have created [Avenger](https://github.com/buildo/avenger). It's a powerful data-fetching library supporting batching, caching, data dependencies and much more. Refer to the [Avenger book](https://buildo.gitbooks.io/avenger/content/docs/introduction/Overview.html) for more details.

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

```
import { Query } from 'avenger';
import t from 'tcomb';
import * as API from 'API';

const queries = {

  user: Query({
    id: 'user',
    returnType: t.Any,
    fetch: API.getUser
  })

};

export default queries;
```

## More react-container magic

In `HelloContainer.js` you can now ask `react-container` to bind our `Hello` component to the *Avenger* query you have just created.

Use the alternative _"factory"_ invocation of `react-container`:

```js
import containerFactory from 'react-container';
import allQueries from 'queries';

const container = containerFactory({ allQueries });
```

Then invoke `container()` as before, with an additional `queries: ['user']` property. This will add a new `user` property to the input of `mapProps()`.

```
const HelloContainer = container(Hello, {
  connect: { formal: t.maybe(t.Boolean) },
  queries: ['user'],
  mapProps: ({ transition, formal = false, user }) => ({
    toggle: () => {
      transition({ formal: !formal });
    },
    formal,
    user: user || '...'
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
getLocals() {
  const { toggle, user } = this.props;
  const greeting = this.props.formal ? this.formalGreeting() : 'Hello';

  return { toggle, greeting, user };
}
```

And finally render it!

```js
template({ toggle, greeting, user }) {
  return (
    <div className='hello'>
      <h1>
        <a onClick={toggle}>{greeting}</a> {user}
      </h1>
    </div>
  );
}
```

## Step3->Step4

Check the [full diff](https://github.com/buildo/webseed/compare/tutorial-step3...tutorial-step4) between Step 3 and Step 4.