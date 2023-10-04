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

### Subprojects (git-subtree)

- [src/jomiel-proto/](src/jomiel-proto/) of [jomiel-proto]

[jomiel-proto]: https://github.com/guendto/jomiel-proto/
