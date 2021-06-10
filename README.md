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

### Note for devs

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
  StatusCode
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

## License

`jomiel-messages` is licensed under the [Apache License version
2.0][aplv2].

[aplv2]: https://www.tldrlegal.com/l/apache2

## Acknowledgements

### Subprojects (git-subtree)

- [src/jomiel-proto/](src/jomiel-proto/) of [jomiel-proto]

[jomiel-proto]: https://github.com/guendto/jomiel-proto/
