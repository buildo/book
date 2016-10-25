# Step 6

A common pattern for components rendering server data is showing a spinner while data is being saved/loaded. `react-container` supports a `loadingDecorator` property that will handle most of this for you. We usually pair it with [react-avenger/loading](https://github.com/buildo/react-avenger/blob/master/loading.js), a 

Add the property like this:

```js
loadingDecorator: myLoadingComponent
```

where `myLoadingComponent` is a React component that will receive some useful props like `ready`, `loading` and `readyState`.

## Using the loading() helper

To simplify creating the `loadingComponent` we usually rely on [react-avenger/loading](https://github.com/buildo/react-avenger/blob/master/loading.js), a helper accepting two params: `wrapper` and `loader`.

Import it with
```js
import loading from 'react-avenger/loading'; 
```

Then use it like this:
```js
const myLoadingComponent = loading({
  wrapper: <div style={{ textAlign: 'center', position: 'relative', minHeight: 100 }} />,
  loader: <LoadingSpinner size='medium' />
});
```

## Using the LoadingSpinner UI component

We also have a reusable React component to drop a nicer animated spinner in a matter of seconds. It's part of our suite of shared [react-components](https://github.com/buildo/react-components/). Import it like this:

```js
import LoadingSpinner from 'buildo-react-components/src/loading-spinner';
import 'buildo-react-components/blob/master/src/loading-spinner/loadingSpinner.scss';
```

Then replace `<div>loading...</div>` with `<LoadingSpinner size='medium' />`. Et voilà!

## Step5->Step6

Check the [full diff](https://github.com/buildo/webseed/compare/tutorial-step5...tutorial-step6) between Step 5 and Step 6.