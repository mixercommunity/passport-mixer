# passport-beam
[Passport](http://passportjs.org/) strategies for authenticating with [Mixer.com](https://www.Mixer.com/).

This module lets you authenticate using Mixer.com in your Node.js applications.
By plugging into Passport, Mixer.com authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-mixer

#### Configure Strategy

The Mixer.com OAuth authentication strategy authenticates users using a Mixer.com
account and OAuth tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    passport.use(new MixerStrategy({
        clientID: MIXER_CLIENT_ID,
        clientSecret: MIXER,
        callbackURL: "http://127.0.0.1:3000/auth/mixer/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ mixerId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'mixer'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/mixer',
      passport.authenticate('mixer'));

    app.get('/auth/mixer/callback',
      passport.authenticate('mixer', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## License

The MIT License (MIT)

Copyright (c) 2019 AlfW

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON INFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
