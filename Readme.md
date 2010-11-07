# facebook-js

Easy peasy facebook client for connect.

    npm install facebook-js

## Usage

facebook-js has two methods.

* getAccesToken(_params_, _callback_): Uses oAuth module to retrieve the access_token
* apiCall(_http_method_, _path_, _params_, _callback_): Does a call to facebook graph API.

## Example using express.js

    app.get('/facebook/me', function (req, res) {
      var facebookClient = require('facebook-js')('consumerKey', 'consumerSecret');

      facebookClient.getAccessToken({
          redirect_uri: 'http://localhost:3000/facebook/auth',
          code: req.param('code'),
          scope: 'offline_access,read_stream,publish_stream'
        },
        function (error, token) {
          facebookClient.graphCall('GET', '/me', {access_token: token.access_token}, function (error, result) {
            res.render('facebook_me.jade', {locals: {result: result}});
          });
        }
      );
    });
