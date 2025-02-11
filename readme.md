# unist-util-visit [![Build Status][build-badge]][build-page] [![Coverage Status][coverage-badge]][coverage-page]

[Unist][] node visitor.  Useful with working with [**remark**][remark]
or [**retext**][retext].

## Installation

[npm][]:

```bash
npm install unist-util-visit
```

**unist-util-visit** is also available as an AMD, CommonJS, and
globals module, [uncompressed and compressed][releases].

## Usage

Dependencies:

```javascript
var remark = require('remark');
var visit = require('unist-util-visit');

remark().use(function () {
    return function (ast) {
        visit(ast, 'text', function (node) {
          console.log(node)
        });
    };
}).process('Some _emphasis_, **strongness**, and `code`.');
```

Yields:

```js
{'type': 'text', 'value': 'Some '}
{'type': 'text', 'value': 'emphasis'}
{'type': 'text', 'value': ', '}
{'type': 'text', 'value': 'strongness'}
{'type': 'text', 'value': ', and '}
{'type': 'text', 'value': '.'}
```

## API

### `visit(node[, type], visitor[, reverse])`

Visit nodes. Optionally by node type. Optionally in reverse.

*   `node` ([`Node`][node])
    — Node to search;

*   `type` (`string`, optional)
    — Node type;

*   `visitor` ([Function][visitor])
    — Visitor invoked when a node is found;

*   `reverse` (`boolean`, default: `false`)
    — When falsey, checking starts at the first child and continues
    through to later children.  When truthy, this is reversed.

    This **does not** mean checking starts at the deepest node and
    continues on to the highest node.

#### `stop? = visitor(node, index, parent)`

Invoked when a node (when `type` is given, matching `type`) is found.

**Parameters**:

*   `node` (`Node`) — Found node;
*   `index` (`number?`) — Position of `node` in `parent`;
*   `index` (`Node?`) — Parent of `node`.

**Returns**: `boolean?` - When `false`, visiting is immediately stopped.

## License

[MIT][license] © [Titus Wormer][author]

<!-- Definition -->

[build-badge]: https://img.shields.io/travis/wooorm/unist-util-visit.svg

[build-page]: https://travis-ci.org/wooorm/unist-util-visit

[coverage-badge]: https://img.shields.io/codecov/c/github/wooorm/unist-util-visit.svg

[coverage-page]: https://codecov.io/github/wooorm/unist-util-visit?branch=master

[npm]: https://docs.npmjs.com/cli/install

[releases]: https://github.com/wooorm/unist-util-visit/releases

[license]: LICENSE

[author]: http://wooorm.com

[unist]: https://github.com/wooorm/unist

[retext]: https://github.com/wooorm/retext

[remark]: https://github.com/wooorm/remark

[node]: https://github.com/wooorm/unist#node

[visitor]: #stop--visitornode-index-parent
