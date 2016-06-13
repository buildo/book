# Step 7

At buildo, we are not TDD integralists but we believe adding new unit tests should be as painless as possible. This is why the boilerplate includes all you need to get started. This is all the code you need to add in ` test/tests/components/Hello.js` to create a couple of runnable tests for our UI component.

```js
import Hello from 'components/Hello/Hello.js';
import expect from 'expect';

const baseProps = {
  toggle: () => {},
  user: 'user',
  onRefreshClick: () => {}
};

describe('Hello', () => {

  it('should greet in an informal way when formal=false', () => {

    const hello = new Hello({ ...baseProps, formal: false });
    expect(hello.getLocals().greeting).toBe('Hello');

  });

  it('should greet in a formal way when formal=true', () => {

    const hello = new Hello({ ...baseProps, formal: true });
    expect(hello.getLocals().greeting.includes('Good')).toBe(true);

  });

});
```

We rely on the fact that all the logic is encapsulated in the `getLocals()` function and we don't render real DOM elements for our tests.

To run all your tests, just use `npm test`.

## Step6->Step7

Check the [full diff](https://github.com/buildo/webseed/compare/tutorial-step6...tutorial-step7) between Step 6 and Step 7.