babel-plugin-add-module-exports
---

<p align="right">
  <a href="https://npmjs.org/package/babel-plugin-add-module-exports">
    <img src="https://img.shields.io/npm/v/babel-plugin-add-module-exports.svg?style=flat-square">
  </a>
  <a href="https://travis-ci.org/59naga/babel-plugin-add-module-exports">
    <img src="http://img.shields.io/travis/59naga/babel-plugin-add-module-exports.svg?style=flat-square">
  </a>
  <a href="https://codeclimate.com/github/59naga/babel-plugin-add-module-exports/coverage">
    <img src="https://img.shields.io/codeclimate/github/59naga/babel-plugin-add-module-exports.svg?style=flat-square">
  </a>
  <a href="https://codeclimate.com/github/59naga/babel-plugin-add-module-exports">
    <img src="https://img.shields.io/codeclimate/coverage/github/59naga/babel-plugin-add-module-exports.svg?style=flat-square">
  </a>
</p>

Installation
---

```bash
npm install babel-plugin-add-module-exports --save-dev
```

Why?
---

Babel@6 doesn't export default `module.exports` any more - [T2212 *Kill CommonJS default export behavior*](https://phabricator.babeljs.io/T2212).

Babel@6 transforms the following file

```js
// index.js
export default 'foo'
```

into

```js
'use strict';
Object.defineProperty(exports, "__esModule", {
  value: true
});
exports.default = 'foo';
```

Therefore, it is a need to use the ugly `.default` in node.js.

```js
require('./bundle.js') // { default: 'foo' }
require('./bundle.js').default // 'foo'
```

This plugin follows the babel@5 behavior - add the `module.exports` if **only** the `export default` declaration exists.

```js
'use strict';
Object.defineProperty(exports, "__esModule", {
  value: true
});
exports.default = 'foo';
module.exports = exports['default'];
```

Therefore, our old codes still work fine - the `.default` goes away. :wink:

```js
require('./bundle.js') // foo
```

License
---
[MIT](http://59naga.mit-license.org/)
