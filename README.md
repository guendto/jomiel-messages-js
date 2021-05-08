# jomiel-messages-js

The javascript bindings for the [jomiel] protobuf messages.

## About

- Easy to install [jomiel] protobuf message bindings for js
- Generated from the [jomiel-proto] declarations

[jomiel]: https://github.com/guendto/jomiel

## Installation

```shell
npm install jomiel-messages
```

## Usage

Serialize an inquiry message:

```javascript
const { Inquiry } = require("jomiel-messages").jomiel.protobuf.v1beta1;
// uri: a string to inquire
const msg = Inquiry.create({ media: { inputUri: uri } });
const bytes = Inquiry.encode(msg).finish();
// ...
```

De-serialize the response message:

```javascript
const {
  Response,
  StatusCode,
} = require("jomiel-messages").jomiel.protobuf.v1beta1;

// bytes: data read from the socket
const msg = Response.decode(bytes);

if (msg.status.code != StatusCode.STATUS_CODE_OK) {
  console.error(`message=msg.status.message`);
  console.error(`status-code=msg.status.code`);
  console.error(`error-code=msg.status.error`);
  console.error(`http-code=msg.status.http.code`);
  // ...
} else {
  // ...
}
```

## Building packages from repo

```shell
git clone https://github.com/guendto/jomiel-messages-js
cd jomiel-messages-js
npm install
npm [pack|link|publish|...]
```

### Note

We have the following devDependencies in the package.json:

- chalk
- jsdoc
- minimist
- semver
- uglify-js

pbjs (which ./bin/gen-static calls) will otherwise pull these deps
on-demand when it is run -- which is less than ideal.

- See also <https://github.com/protobufjs/protobuf.js/issues/1368>

## License

`jomiel-messages` is licensed under the [Apache License version
2.0][aplv2].

[aplv2]: https://www.tldrlegal.com/l/apache2

## Acknowledgements

### Subprojects (git-subtree)

- [src/jomiel-proto/](src/jomiel-proto/) of [jomiel-proto]

[jomiel-proto]: https://github.com/guendto/jomiel-proto/
