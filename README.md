# @feathersjs/authentication-oauth1

> __Important:__ The code for this module has been moved into the main Feathers repository at [feathersjs/feathers](https://github.com/feathersjs/feathers) ([package direct link](https://github.com/feathersjs/feathers/tree/master/packages/authentication-oauth1)). Please open issues and pull requests there. No changes in your existing Feathers applications are necessary.

[![Build Status](https://travis-ci.org/feathersjs/authentication-oauth1.png?branch=master)](https://travis-ci.org/feathersjs/authentication-oauth1)

> A Feathers OAuth1 authentication strategy

## Installation

```
npm install @feathersjs/authentication-oauth1 --save
```

## Quick example

```js
const feathers = require('@feathersjs/feathers');
const authentication = require('feathers-authentication');
const jwt = require('feathers-authentication-jwt');
const oauth1 = require('@feathersjs/authentication-oauth1');
const session = require('express-session');
const TwitterStrategy = require('passport-twitter').Strategy;
const app = feathers();

// Setup in memory session
app.use(session({
  secret: 'super secret',
  resave: true,
  saveUninitialized: true
}));

// Setup authentication
app.configure(authentication(settings));
app.configure(jwt());
app.configure(oauth1({
  name: 'twitter',
  Strategy: TwitterStrategy,
  consumerKey: '<your consumer key>',
  consumerSecret: '<your consumer secret>'
}));

// Setup a hook to only allow valid JWTs to authenticate
// and get new JWT access tokens
app.service('authentication').hooks({
  before: {
    create: [
      authentication.hooks.authenticate(['jwt'])
    ]
  }
});
```

## Documentation

Please refer to the [@feathersjs/authentication-oauth1 documentation](http://docs.feathersjs.com/) for more details.

## License

Copyright (c) 2018

Licensed under the [MIT license](LICENSE).
