# Step 0

Start by cloning [webseed](https://github.com/buildo/webseed) which includes all the boilerplate you need.


You should be able to do:

```sh
git clone https://github.com/buildo/webseed
cd webseed
npm i
npm start
```

If everything works, your app should be running at http://localhost:8080/.

Under the hood, this basic project is a very simple React component, which you can find at `src/app/components/Hello/Hello.tsx`:

```tsx
import * as React from 'react';
import { intlMethods } from 'Basic';

import './hello.scss';

@intlMethods
export default class Hello extends React.PureComponent {

  formatMessage: (k: string) => string;

  render() {
    return (
      <div className='hello'>
        <h1>{this.formatMessage('Hello.hello')}</h1>
      </div>
    );
  }

}
```

There are a couple of things to note here:
* CSS rules specific to this component are maintained as a `.scss` file in the same folder
* The component is a `React.PureComponent`, meaning that it overrides `shouldComponentUpdate` with a more performant implementation. It only works *pure* components (i.e., componentes that are always rendered in the same way given the same props). In some of our projects you could also see the `@pure` decorator: it does the same thing but it is deprecated, as described [here](../3.first-party_js_libraries.md)
