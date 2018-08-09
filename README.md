# passport-provided

[![Build](https://travis-ci.org/TGNThump/passport-provided.png)](https://travis-ci.org/TGNThump/passport-provided)
[![Dependencies](https://david-dm.org/TGNThump/passport-provided.png)](https://david-dm.org/TGNThump/passport-provided)


[Passport](http://passportjs.org/) strategy for authenticating with a provided username
and password.

This module lets you authenticate using a username and password in your Node.js
applications.  By plugging into Passport, local authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

```bash
$ npm install passport-provided
```

## Usage

#### Configure Strategy

The provided local authentication strategy authenticates users using a username and
password.  The strategy requires a `verify` callback, which accepts these
credentials and calls `done` providing a user.

```js
passport.use(new ProvidedStrategy(
  function(username, password, done) {
    User.findOne({ username: username }, function (err, user) {
      if (err) { return done(err); }
      if (!user) { return done(null, false); }
      if (!user.verifyPassword(password)) { return done(null, false); }
      return done(null, user);
    });
  }
));
```

##### Available Options

This strategy takes an optional options hash before the function, e.g. `new LocalStrategy({/* options */, callback})`.

The available parameters are:

* `username` - the username to attempt login with.
* `password` - the password to attempt login with.
* `session` - use sessions? (default: true)

```javascript
passport.use(new ProvidedStrategy({
    username: 'TGNThump',
    password: 'passwd',
    session: false
  },
  function(username, password, done) {
    // ...
  }
));
```

The verify callback can be supplied with the `request` object by setting
the `passReqToCallback` option to true, and changing callback arguments
accordingly.

    passport.use(new ProvidedStrategy({
        username: 'TGNThump',
        username: 'passwd',
        passReqToCallback: true,
        session: false
      },
      function(req, username, password, done) {
        // request object is now first argument
        // ...
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'local'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

```js
app.post('/login', 
  passport.authenticate('local', { failureRedirect: '/login' }),
  function(req, res) {
    res.redirect('/');
  });
```

## Tests

```bash
$ npm install
$ npm test
```

## Credits

- [Jared Hanson](http://github.com/jaredhanson)
- [Ben Pilgrim](http://github.com/TGNThump)

## License

[The MIT License](http://opensource.org/licenses/MIT)
