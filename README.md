Enzyme Modern
=======

[![npm Version](https://img.shields.io/npm/v/enzyme-modern.svg)](https://www.npmjs.com/package/enzyme-modern) [![License](https://img.shields.io/npm/l/enzyme-modern.svg)](https://github.com/sabaoongfx/enzyme/blob/master/LICENSE.md)

Modernized fork of [Enzyme](https://github.com/enzymejs/enzyme) — the original project was abandoned and is no longer maintained.

Enzyme is a JavaScript Testing utility for React that makes it easier to test your React Components' output.
You can also manipulate, traverse, and in some ways simulate runtime given the output.

Enzyme's API is meant to be intuitive and flexible by mimicking jQuery's API for DOM manipulation
and traversal.

## Why this fork?

The original `enzyme` package has been abandoned and no longer receives updates. `enzyme-modern` is an actively maintained fork that:

- Publishes under the `enzyme-modern` package name
- Keeps dependencies up to date
- Aims to add support for React 17, 18, and 19

## Installation

```bash
npm i --save-dev enzyme-modern enzyme-modern-adapter-react-16
```

Each adapter may have additional peer dependencies which you will need to install as well. For instance,
`enzyme-modern-adapter-react-16` has peer dependencies on `react` and `react-dom`.

### Adapters

| Adapter Package | React compatibility |
| --- | --- |
| `enzyme-modern-adapter-react-16` | `^16.4.0-0` |

Configure enzyme to use your adapter:

```js
import Enzyme from 'enzyme-modern';
import Adapter from 'enzyme-modern-adapter-react-16';

Enzyme.configure({ adapter: new Adapter() });
```

## Basic Usage

### [Shallow Rendering](/docs/api/shallow.md)

```javascript
import React from 'react';
import { expect } from 'chai';
import { shallow } from 'enzyme-modern';

import MyComponent from './MyComponent';
import Foo from './Foo';

describe('<MyComponent />', () => {
  it('renders three <Foo /> components', () => {
    const wrapper = shallow(<MyComponent />);
    expect(wrapper.find(Foo)).to.have.lengthOf(3);
  });

  it('renders an `.icon-star`', () => {
    const wrapper = shallow(<MyComponent />);
    expect(wrapper.find('.icon-star')).to.have.lengthOf(1);
  });

  it('renders children when passed in', () => {
    const wrapper = shallow((
      <MyComponent>
        <div className="unique" />
      </MyComponent>
    ));
    expect(wrapper.contains(<div className="unique" />)).to.equal(true);
  });

  it('simulates click events', () => {
    const onButtonClick = sinon.spy();
    const wrapper = shallow(<Foo onButtonClick={onButtonClick} />);
    wrapper.find('button').simulate('click');
    expect(onButtonClick).to.have.property('callCount', 1);
  });
});
```

Read the full [API Documentation](/docs/api/shallow.md)

### [Full DOM Rendering](/docs/api/mount.md)

```javascript
import React from 'react';
import sinon from 'sinon';
import { expect } from 'chai';
import { mount } from 'enzyme-modern';

import Foo from './Foo';

describe('<Foo />', () => {
  it('allows us to set props', () => {
    const wrapper = mount(<Foo bar="baz" />);
    expect(wrapper.props().bar).to.equal('baz');
    wrapper.setProps({ bar: 'foo' });
    expect(wrapper.props().bar).to.equal('foo');
  });

  it('simulates click events', () => {
    const onButtonClick = sinon.spy();
    const wrapper = mount((
      <Foo onButtonClick={onButtonClick} />
    ));
    wrapper.find('button').simulate('click');
    expect(onButtonClick).to.have.property('callCount', 1);
  });

  it('calls componentDidMount', () => {
    sinon.spy(Foo.prototype, 'componentDidMount');
    const wrapper = mount(<Foo />);
    expect(Foo.prototype.componentDidMount).to.have.property('callCount', 1);
    Foo.prototype.componentDidMount.restore();
  });
});
```

Read the full [API Documentation](/docs/api/mount.md)

### [Static Rendered Markup](/docs/api/render.md)

```javascript
import React from 'react';
import { expect } from 'chai';
import { render } from 'enzyme-modern';

import Foo from './Foo';

describe('<Foo />', () => {
  it('renders three `.foo-bar`s', () => {
    const wrapper = render(<Foo />);
    expect(wrapper.find('.foo-bar')).to.have.lengthOf(3);
  });

  it('renders the title', () => {
    const wrapper = render(<Foo title="unique" />);
    expect(wrapper.text()).to.contain('unique');
  });
});
```

Read the full [API Documentation](/docs/api/render.md)

## React Hooks support

Enzyme supports [react hooks](https://reactjs.org/docs/hooks-intro.html) with some limitations in [`.shallow()`](https://enzymejs.github.io/enzyme/docs/api/shallow.html) due to upstream issues in React's shallow renderer:

* `useEffect()` and `useLayoutEffect()` don't get called in the React shallow renderer. [Related issue](https://github.com/facebook/react/issues/15275)

* `useCallback()` doesn't memoize callback in React shallow renderer. [Related issue](https://github.com/facebook/react/issues/15774)

### [`ReactTestUtils.act()`](https://reactjs.org/docs/test-utils.html#act) wrap

If you're using React 16.8+ and `.mount()`, Enzyme will wrap apis including [`.simulate()`](https://enzymejs.github.io/enzyme/docs/api/ReactWrapper/simulate.html), [`.setProps()`](https://enzymejs.github.io/enzyme/docs/api/ReactWrapper/setProps.html), [`.setContext()`](https://enzymejs.github.io/enzyme/docs/api/ReactWrapper/setContext.html), [`.invoke()`](https://enzymejs.github.io/enzyme/docs/api/ReactWrapper/invoke.html) with [`ReactTestUtils.act()`](https://reactjs.org/docs/test-utils.html#act) so you don't need to manually wrap it.

## Packages

| Package | npm |
|---------|-----|
| `enzyme-modern` | [![npm](https://img.shields.io/npm/v/enzyme-modern.svg)](https://www.npmjs.com/package/enzyme-modern) |
| `enzyme-modern-shallow-equal` | [![npm](https://img.shields.io/npm/v/enzyme-modern-shallow-equal.svg)](https://www.npmjs.com/package/enzyme-modern-shallow-equal) |
| `enzyme-modern-adapter-utils` | [![npm](https://img.shields.io/npm/v/enzyme-modern-adapter-utils.svg)](https://www.npmjs.com/package/enzyme-modern-adapter-utils) |
| `enzyme-modern-adapter-react-16` | [![npm](https://img.shields.io/npm/v/enzyme-modern-adapter-react-16.svg)](https://www.npmjs.com/package/enzyme-modern-adapter-react-16) |

## Contributing

See the [Contributors Guide](/CONTRIBUTING.md)

## License

[MIT](/LICENSE.md)
