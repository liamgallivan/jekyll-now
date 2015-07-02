---
layout: post
title: Using Yelp API
---

#How to make api requests to yelp
Yelp is a very popular small business and restaraunt review site. Many use it 
to make descisions on where they eat or buy things, trusting fellow users to 
guide their descisions. Here is  guide to properly requesting to the api.

First you will want to set up a yelp account and request authentication keys.


Yelp uses OAuth to authenticate transactions so you will need a comunsumer key
and secret as well as a token key and secret. Now comes writing the request.

The request will be a jsonp ajax request and for the sake of this tutorial
i will be using the $http function in angular to create my requests.

Below is the code of a basic request, with the Oauth params included.

```javascript
var url = 'http://api.yelp.com/v2/search';
var method = 'GET';
var consumerSecret = CONSUMERSECRET
var tokenSecret = TOKENSECRET
vr params = {
	location:TARGETCITY
	callback: 'angular.callbacks._0',
	oauth_consumer_key: CONSUMERKEY
	oauth_token: TOKENKEY,
	oauth_signature_method: "HMAC-SHA1",
	oauth_timestamp: time,
	oauth_version: '1.0',
	oauth_nonce: randomString(32, '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ')
};
var signature = oauthSignature.generate(method, url, params, consumerSecret, tokenSecret, { encodeSignature: true});
params.oauth_signature = signature;
$http.jsonp(url, {params:params}).success;
```
Some key points that will not be found in the yelp API documentation are
that a library will be needed to create an Oauth signature, and that signature 
will have to be added to the Params you are passing to the request.