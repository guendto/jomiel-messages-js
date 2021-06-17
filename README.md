# jomiel-messages-js

[![npm-package](https://img.shields.io/npm/v/jomiel-messages?color=%230a66dc)][npm]
[![code-style](https://img.shields.io/badge/code%20style-prettier+eslint-%230a66dc)][prettier-eslint]

The javascript bindings for the [jomiel] protobuf messages.

- Easy to install [jomiel] protobuf message bindings for js
- Generated from the [jomiel-proto] declarations

[prettier-eslint]: http://npm.im/prettier-eslint
[npm]: https://npm.im/jomiel-messages
[jomiel]: https://github.com/guendto/jomiel

## Installation

```shell
npm install jomiel-messages
```

## Usage

Serialize an inquiry message:

```javascript
import jomielMessages from "jomiel-messages";

const { Inquiry } = jomielMessages.jomiel.protobuf.v1beta1;
const uri = "https://...";

const msg = Inquiry.create({ media: { inputUri: uri } });
const bytes = Inquiry.encode(msg).finish();

// ...
```

Deserialize the response message:

```javascript
const { Response, StatusCode } = jomielMessages.jomiel.protobuf.v1beta1;

// bytes: data read from the zeromq socket (returned by jomiel)
const msg = Response.decode(bytes);

if (msg.status.code !== StatusCode.STATUS_CODE_OK) {
  const status = msg.status;
  // ...
}
```

## License

`jomiel-messages` is licensed under the [Apache License version
2.0][aplv2].

[aplv2]: https://www.tldrlegal.com/l/apache2

## Acknowledgements

### Additional devDependencies in package.json

The following **devDependencies** are installed to prevent [pbjs] --
which is what ./bin/[gen-static] calls -- from installing them
on-demand:

- chalk
- jsdoc
- minimist
- semver
- uglify-js

See also protobufjs issue [#1368].

[gen-static]: https://github.com/guendto/jomiel-messages-js/blob/master/bin/gen-static
[pbjs]: https://github.com/protobufjs/protobuf.js/
[#1368]: https://github.com/protobufjs/protobuf.js/issues/1368

### Subprojects (git-subtree)

- [src/jomiel-proto/](src/jomiel-proto/) of [jomiel-proto]

[jomiel-proto]: https://github.com/guendto/jomiel-proto/
