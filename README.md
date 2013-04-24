# Passport-bitly

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [bitly](http://bitly.com/) using the OAuth 2.0 API.

This module lets you authenticate using bitly, in your Node.js applications.
By plugging into Passport, bitly
authentication can be easily and unobtrusively integrated into any application or
framework that supports [Connect](http://www.senchalabs.org/connect/)-style
middleware, including [Express](http://expressjs.com/).

[![Build Status](https://travis-ci.org/dreadjr/passport-bitly.png?branch=master)](https://travis-ci.org/dreadjr/passport-bitly)

## Install

    $ npm install passport-bitly

## Usage

#### Configure Strategy

The bitly authentication strategy authenticates users using a bitly
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    passport.use(new BitlyStrategy({
        clientID: BITLY_CLIENT_ID,
        clientSecret: BITLY_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/bitly/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ bitlyId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'bitly'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/bitly',
      passport.authenticate('bitly'));

    app.get('/auth/bitly/callback',
      passport.authenticate('bitly', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Examples

For a complete, working example, refer to the [login example](https://github.com/dreadjr/passport-bitly/tree/master/examples/login).


## Credits

  - [dreadjr](http://github.com/dreadjr)


## Thanks

  - [Jared Hanson](http://github.com/jaredhanson)


## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2013 dreadjr
