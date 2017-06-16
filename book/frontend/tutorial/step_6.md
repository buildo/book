# Step 6

A common pattern for components rendering server data is showing a spinner while data is being saved/loaded. Currently, we are just using the `noLoaderLoading` workaround, but there is a `@loading` decorator that will handle most of this loading feature for you ([react-avenger/loading](https://github.com/buildo/react-avenger/blob/master/src/loading.js). We usually pair it with the b-r-c [loadingSpinner](https://github.com/buildo/react-components/tree/master/src/loading-spinner).

## Using the loading() helper

Import the loading helper with:
```js
import loading from 'react-avenger/lib/loading';
```

Then use it as a decorator of the `Hello.js` component, replacing the `@noLoaderLoading` one with this:
```js
@loading({
  wrapper: <div style={{ textAlign: 'center', position: 'relative', minHeight: 100 }} />,
  loader: <div>loading...</div>
})
```

## Using the LoadingSpinner UI component

We also have a reusable React component to drop a nicer animated spinner in a matter of seconds. It's part of our suite of shared [react-components](https://github.com/buildo/react-components/). Let's include it in out project by following the [guidelines](../guidelines/5.buildo-react-components.md).

1. Create a `src/app/components/Basic/LoadingSpinner/LoadingSpinner.js` file:
```js
import './loadingSpinner.scss';

export default from 'buildo-react-components/lib/loading-spinner';
```

2. Export it through an `index.js` file in the same folder:
```js
export default from './LoadingSpinner';
```

3. Import it's style in the `loadingSpinner.scss` file:
```css
@import '~buildo-react-components/src/loading-spinner/loadingSpinner.scss';
```

4. Make it part of our set of Basic, reusable, components, by adding a line to `src/app/components/Basic/index.js`:
```js
export LoadingSpinner from './LoadingSpinner';
```

We can now import it in the `Hello.js` component as follows:
```js
import { LoadingSpinner } from 'Basic';
```

And replace the `<div>loading...</div>` in `@loading` with `<LoadingSpinner />`. Et voilà!

## Step5 -> Step6 diff

You can check the `Step 6` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
