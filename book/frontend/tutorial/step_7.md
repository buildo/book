# Step 7

In the previous step we included a components from our [react-components](https://github.com/buildo/react-components/)by following the [guidelines](../guidelines/5.buildo-react-components.md) that we defined in this book. However, there was no customization involved.

In this step we will improve the UI of our beloved `Hello` component using the b-r-c [Panel](https://github.com/buildo/react-components/tree/master/src/Panel), customized specifically for this project.

## Creating the Basic Panel component

Let's perform the same steps that we did previously for the loading spinner, but this time adding some customization on top of the standard b-r-c component:

Create a `src/app/components/Basic/Panel/Panel.tsx` file as follows:

```tsx
import * as React from 'react';
import { default as BRCPanel, PanelProps } from 'buildo-react-components/lib/Panel/Panel';
import { ObjectOmit } from 'typelevel-ts';

import './panel.scss';

type DefaultProps = {
  type: PanelProps['type']
};

type RequiredProps = ObjectOmit<PanelProps, keyof DefaultProps>;

type Props = Partial<DefaultProps> & RequiredProps;

const defaultProps: DefaultProps = {
  type: 'docked-top'
};

export default class Panel extends React.PureComponent<Props> {

  getProps() {
    return { ...defaultProps, ...this.props };
  }

  render() {
    return <BRCPanel {...this.getProps()} />;
  }

}
```

In this way we already customized the `BRCPanel` by saying that we want the `Basic` `Panel` of this project to always be `docked-top`.
To do it, we had to do some TypeScript magic:
1. We defined the `DefaultProps` type, to tell TypeScript that the `defaultProps` that we are defining here (only `type` in this case) have the same type of the corresponding `Panel` properties (extracted from `PanelProps`)
2. Omit `DefaultProps` from `PanelProps` and re-add them to the same type by making them optional thanks to `Partial`, as follows: `type Props = Partial<DefaultProps> & RequiredProps;`. `Partial` makes all properties of a type optional

In this way we exposed the properties we defaulted as optional, no matter if they were such or not in the `BRCPanel` component: we gave `type` a value and made the `type` prop optional, so that it can be overridden but it doesn't have to.

Now, export the component through an `index.ts` file in the same folder:

```ts
import Panel from './Panel';
export default Panel;
```

and import its style in the `panel.scss` file, customizing it using the SASS interface:

```scss
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

Finally, make it part of our set of Basic, reusable, components, by adding a line to `src/app/components/Basic/index.ts`:

```ts
import Panel from './Panel';
export { Panel };
```

## Using it inside Hello.tsx

Let's now sorround the `Hello` div with a `Panel`.
We can import it from `Basic`:

```ts
import { LoadingSpinner, Panel } from 'Basic';
```

And then use it directly in the `render` method:

```tsx
<Panel className='hello'>
  <div>
    <h1>
      <a onClick={toggle}>{greeting}</a> {user}
    </h1>
    <a onClick={onRefreshClick}>(refresh)</a>
  </div>
</Panel>
```

You will see that the layout still has some problems.
We need to adjust the `hello.scss` file:

```scss
.hello {
  div {
    color: $coolBlue;
    text-align: center;
  }
}
```

And the `src/app/theme/main.scss`:

```scss
.layout,
.layout > div {
  height: 100%;
  max-width: 1000px;
  margin: 0 auto;
}
```

## Step6 -> Step7 diff

You can check the `Step 7` commit diff [here](https://github.com/buildo/webseed/commits/tutorial).
