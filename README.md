# hood

Cover your head.

Security headers middleware.

## Usage

```js
var hood = require('hood');
app.use(hood());
```

This will setup sane defaults for most apps. You can also pass options to configure each middleware.

```js
app.use(hood({
  csp: "default-src 'unsafe-inline'",
  hsts: false // pass false to disable a middlware
}));
```

Each middleware is also available individually.

### csp

```js
app.use(hood.csp());
app.use(hood.csp({
  policy: {
    'default-src': ['self', 'unsafe-inline']
  }
}));
app.use(hood.csp("default-src 'self';"));
```

### hsts

```js
app.use(hood.hsts());
app.use(hood.hsts({
  maxAge: 1000, // seconds
  includeSubdomains: true // default false
}));
app.use(hood.hsts(1000, true));
```

### xframe

````js
app.use(hood.xframe()) // DENY
app.use(hood.xframe({
  sameOrigin: true
}));
app.use(hood.xframe({
  allow: 'http://example.domain'
}));
app.use(hood.xframe('SAMEORIGIN'));
app.use(hood.xframe('ALLOW-FROM http://example.domain'));
```

### header

A convenience method when you need to add arbitrary headers to all requests.

````js
app.use(hood.header('x-foo', 'bar'));
app.use(hood.header({
  'x-foo': 'bar',
  'x-baz': 'quux'
}));
```