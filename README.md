# oauth2-server-jwt

[![Build Status](https://travis-ci.org/compwright/oauth2-server-jwt.svg?branch=master)](https://travis-ci.org/compwright/oauth2-server-jwt) [![Greenkeeper badge](https://badges.greenkeeper.io/compwright/oauth2-server-jwt.svg)](https://greenkeeper.io/)

Storageless JWT token generator backend for [oauth2-server](https://github.com/compwright/node-oauth2-server)

## Features

* Respects oauth2-server token lifetime configuration for each type of token
* Generates JWT access tokens, refresh tokens, and authorization codes

## Limitations

For proper verification of `aud`, `scope`, and `redirectUri`, you will need to implement [`model.getClient()`](https://oauth2-server.readthedocs.io/en/latest/model/spec.html#getclient-clientid-clientsecret-callback) separately.

If you need to support the `password` grant type, you will also need to implement [`model.getUser()`](https://oauth2-server.readthedocs.io/en/latest/model/spec.html#getuser-username-password-callback) separately.

Suggested implementation: [oauth2-server-mongoose](https://github.com/compwright/oauth2-server-mongoose)

## Requirements

* Node.js 8+
* [oauth2-server](https://github.com/compwright/node-oauth2-server)

## Installation

```bash
$ npm install --save @compwright/oauth2-server oauth2-server-jwt
```

## Usage

```javascript
const OAuth2Server = require('@compwright/oauth2-server');
const jwtMixin = require('oauth2-server-jwt');
const mongooseMixin = require('oauth2-server-mongoose');

const oauth = new OAuth2Server({
    model: {
        ...jwtMixin({
            accessTokenSecret,                  // String (required)
            refreshTokenSecret,                 // String (required)
            authorizationCodeSecret,            // String (required)
            issuer,                             // String (required)
            userId: 'id'                        // String
            algorithms: ['HS256']               // Array[String]
        }),
        ...mongooseMixin()
    }
});
```

## License

MIT license
