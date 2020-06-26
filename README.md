# postman-imgur
Using Postman with Oauth2 and refreshing its token automatically using pre-request scripts


## Step-by-Step

### Collection creation

I created a collection `imgur` and a folder `Accounts` under it to put all account related endpoints. It should look like this
![](_img/initial.png) 

### Environment variables
- `baseUrl`: https://api.imgur.com
- `clientId` and `clientSecret`: obtained when you subscribe your app at imgur service
- `accessToken` and `refreshToken`: used to store its respectives values when we get it

### Oauth2 authentication
In this solution, I'll need to get manually the first pair of access and refresh token. After that, I'll refresh automatically when access token expires.

Right clicking at the collection, go to Edit at the context menu, and then to the Authentication tab.
![](_img/oauth_config.png)

Select `Oauth 2.0` as the type of authentication. After that, click on `Get New Access Token` to setup all info, then `Request Token`:

```
Callback URL: https://www.getpostman.com/oauth2/callback
Auth URL: https://api.imgur.com/oauth2/authorize
Access Token URL: https://api.imgur.com/oauth2/authorize
```

![](_img/oauth_get_token.png)

At this moment, you're going to be requested to loggin to imgur and if everythig is ok, you're going to get a Token ready to be used.
![](_img/oauth_use_token.png)

> Note: all requests that need to authenticate, could use `Inherit auth from parent` at its Auth tab. Although, for our purpose, choose the `Bearer Token` option, and fill the Token field with the Enviroment variable `{{accseeToken}}`. This way, every time we change the variable value, the token will be changed in every request.

> Note 2: Either choosing `Inherit auth from parent` or `Bearer Token` an `Authorization` entry will be added to request Header automatically.

### Using the first gotten token
After configuring and getting correctly the first pair of tokens, copy and paste its values to its respectives environment variables.
![](_img/env_variables.png)

Try to run some simple request to see if your basic setup is functioning