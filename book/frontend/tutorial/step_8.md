# Step 8

You reached the last step of the tutorial!

In our projects we almost always use the (FlexView)[https://github.com/buildo/react-flexview] component to compose our layout and to wrap our components, instead of the classic `<div>`. To easily understand why, take a minute to read the introduction of the [Flexview Book](https://buildo.gitbooks.io/flexview/content/docs/Introduction.html).

Let's try to do the same here!

First, to make it work, add the corresponding `import` inside the `src/app/theme/index.ts` file:
```ts
import 'react-flexview/src/flexView.scss';
```
if you forget to import this and try to use `FlexView`, you will have a bad time!

You can now import the component in `Hello.tsx`:
```ts
import FlexView from 'react-flexview';
```

And then pimp your layout with it!
Let's see how easy it is to add two side views to our `Panel` using `FlexView`:
```tsx
<FlexView className='hello'>
  <FlexView basis='150' shrink vAlignContent='center' className='side-view'>
    <h2>I'm the left view!</h2>
  </FlexView>
  <FlexView className='hello-view' grow>
    <Panel>
      <FlexView column hAlignContent='center'>
        <h1>
          <a onClick={toggle}>{greeting}</a> {user}
        </h1>
        <a onClick={onRefreshClick}>(refresh)</a>
      </FlexView>
    </Panel>
  </FlexView>
  <FlexView basis='150' shrink vAlignContent='center' className='side-view'>
    <h2>I'm the right view!</h2>
  </FlexView>
</FlexView>
```

Add also this in `hello.scss`, inside the `.hello` class:
```scss
.side-view {
  margin: 20px;
}
```

And check out the result. If you did something similar before by just using `div`s, you can easily understand why we prefer using `FlexView`. Check out the corresponding [book](https://buildo.gitbooks.io/flexview/content/docs/Introduction.html) to learn more.

🎉🎉 This tutorial ends here, congratulations! 🎉🎉

## Step7 -> Step8 diff

You can check the `Step 8` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
