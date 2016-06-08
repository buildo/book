# Step 0

Start by downloading [this zipfile](https://github.com/buildo/webseed/archive/tutorial-step0.zip) which includes all the boilerplate you need.

The boilerplate is not documented at the moment, so treat it as a black box. There is an [open issue](https://github.com/buildo/webseed/issues/18) about reducing the necessary boilerplate.

You should be able to do:

```sh
unzip webseed-tutorial-step0.zip
cd webseed-tutorial-step0/
cp config-development.json.example config.json
npm i
npm start
```

If everything works, your app should be running at http://localhost:9090/

Under the hood, this is a very simple React component, which you can find at `src/app/components/Hello/Hello.js`:

```js
import React from 'react';
import { pure } from 'revenge';

import './hello.scss';

@pure
export default class Hello extends React.Component {

  render() {
    return (
      <div className='hello'>
        <h1>Hello</h1>
      </div>
    );
  }

}
```

There are a couple of things to note here:
* CSS rules specific to this component are maintained as a `.scss` file in the same folder
* The component is decorated with `@pure`, imported from the [revenge](https://github.com/buildo/revenge) library. This overrides `shouldComponentUpdate` with a more performant implementation, but it only works if your components are pure.