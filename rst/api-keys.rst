.. _api-keys:

API Keys
========

Authorization
-------------
We require that a JSON Web Token `JWT <https://jwt.io/>`_ be sent along with requests via the `Authorization` header. There's no need to create JWTs manually since they will be created for you when you register for the API - Register at |dev_portal_url|

JWTs are passed as bearer tokens in the `Authorization` header, and look like the following::

  Authorization: Bearer <api-key>



Titles
------
The `TitleID` for a request is determined by the API Key and sent in the `Authorization` header automatically. Some objects may have a `titleID` field specifying the game title associated with the data returned.



Rate Limits
-----------
To ensure the availability and stability of the PUBG API, each API key has a limit on the number of requests it can be used to make per minute. The default rate limit is 10 requests per minute for testing/development purposes. When you have exceeded the number of available requests you will receive an HTTP 429 error code (too many requests), but you should be able to make requests again within a minute.

Limit tokens are incrementally filled by 60(sec)/ rate limit. ex: 60(sec)/10(rate) gets rate token every 6 seconds up to max rate limit.

If you need to increase your rate limit, please log into your admin dashboard, find the app you would like a higher rate limit for, and click “request a higher rate limit". Please keep in mind that we require some form of working sample and/or an explanation of the need for a higher limit in order to approve rate limit increase requests.

The rate limit headers are defined as follows:

**X-RateLimit-Limit** - *Request limit per day / per minute*

**X-RateLimit-Remaining** - *The number of requests left for the time window*

**X-RateLimit-Reset** - *The remaining window before the rate limit is refilled in UTC epoch nanoseconds*



Security Considerations
-----------------------
Remember when developing a website/web application that your API key should never be stored client side. Calls to the API should only be made from a secure server side application.
