# Step 7

In the previous step we included a components from our [react-components](https://github.com/buildo/react-components/)by following the [guidelines](../guidelines/5.buildo-react-components.md) that we defined in this book. However, there was no customization involved.

In this step we will improve the UI of our beloved `Hello` component using the b-r-c [Panel](https://github.com/buildo/react-components/tree/master/src/Panel), customized specifically for this project.

## Creating the Basic Panel component

Let's perform the same steps that we did previously for the loading spinner, but this time adding some customization on top of the standard b-r-c component:

1. Create a `src/app/components/Basic/Panel/Panel.js` file as follows:
```js
import React from 'react';
import BRCPanel from 'buildo-react-components/lib/Panel/Panel';
import skinnable from 'react-skinnable';

import './panel.scss';

@skinnable()
export default class Panel extends React.PureComponent {

  template({ type = 'docked-top', ...props }) {
    return <BRCPanel type={type} {...props} />;
  }

}
```
As you can see, we already customized the `BRCPanel` by saying that we want the `Basic` `Panel` of this project to always be `docked-top`.

2. Export it through an `index.js` file in the same folder:
```js
export default from './Panel';
```

3. Import its style in the `panel.scss` file and customize it using the SASS interface:
```css
@import '~theme/variables.scss';

$content-background: $cloud;

@import '~buildo-react-components/src/Panel/panel.scss';

.panel {
  border-radius: 10px;
  box-shadow: 0 2px 0 $darkGrey;

  .panel-content {
    border-radius: 10px;
  }
}
```
We just overridden its default background color, via sass variables override, and customized its border and shadow.

4. Make it part of our set of Basic, reusable, components, by adding a line to `src/app/components/Basic/index.js`:
```js
export Panel from './Panel';
```

## Using it inside Hello.js

Let's now sorround the `Hello` div with a `Panel`.
We can import it from `Basic`:
```js
import { LoadingSpinner, Panel } from 'Basic';
```

And then use it directly in the `template` method:
```js
template({ greeting, toggle, user, onRefreshClick }) {
  <Panel className='hello'>
    <div>
      <h1>
        <a onClick={toggle}>{greeting}</a> {user}
      </h1>
      <a onClick={onRefreshClick}>(refresh)</a>
    </div>
  </Panel>
}
```

You will see that the layout still has some problems.
We need to adjust the `hello.scss` file:
```css
.hello {
  div {
    color: $coolBlue;
    text-align: center;
  }
}
```

And the `src/app/theme/main.scss`:
```css
.layout,
.layout > div {
  height: 100%;
  max-width: 1000px;
  margin: 0 auto;
}
```

## Step6 -> Step7 diff

You can check the `Step 7` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
