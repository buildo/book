# Step 6

A common pattern for components rendering server data is showing a spinner while data is being saved/loaded. Currently, we are just using the `noLoaderLoading` workaround, but there is a `@loading` decorator that will handle most of this loading feature for you ([react-avenger/loading](https://github.com/buildo/react-avenger/blob/master/src/loading.js). We usually pair it with the b-r-c [loadingSpinner](https://github.com/buildo/react-components/tree/master/src/loading-spinner).

## Using the loading helper

Import the loading helper in `Hello.tsx`:

```ts
import _loading from 'react-avenger/lib/loading';
```

Remove the `noLoaderLoading` usage inside the `HelloContainer`, and use instead `loading` to wrap the `Hello` component (export the wrapped component instead of the `Hello` class):

```tsx
const loading = _loading({
  wrapper: <div style={{ textAlign: 'center', position: 'relative', minHeight: 100 }} />,
  loader: <div>loading...</div>
})

export default loading(Hello);
```

## Using the LoadingSpinner UI component

We also have a reusable React component to drop a nicer animated spinner in a matter of seconds. It's part of our suite of shared [react-components](https://github.com/buildo/react-components/). Let's include it in out project by following the [guidelines](../guidelines/5.buildo-react-components.md).

Create a `src/app/components/Basic/LoadingSpinner/LoadingSpinner.ts` file:

```ts
import './loadingSpinner.scss';

import LoadingSpinner from 'buildo-react-components/lib/LoadingSpinner';
export default LoadingSpinner;
```

Export it through an `index.ts` file in the same folder:

```ts
import LoadingSpinner from './LoadingSpinner';
export default LoadingSpinner;
```

Import its style in the `loadingSpinner.scss` file:

```scss
@import '~buildo-react-components/src/LoadingSpinner/loadingSpinner.scss';
```

Make it part of our set of Basic, reusable, components, by adding a line to `src/app/components/Basic/index.ts`:

```ts
import LoadingSpinner from './LoadingSpinner';
export { LoadingSpinner };
```

We can now import it in the `Hello.tsx` component as follows:

```ts
import { LoadingSpinner } from 'Basic';
```

And replace the `<div>loading...</div>` in `loading` with `<LoadingSpinner />`. Et voilà!

## Step5 -> Step6 diff

You can check the `Step 6` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
