.. _rate-limits:

Rate Limits
===========

To ensure the availability and stability of the PUBG API, each API key has a limit on the number of requests it can be used to make per minute. The default rate limit is 10 requests per minute for testing/development purposes. When you have exceeded the number of available requests you will receive an HTTP 429 error code (too many requests), but you should be able to make requests again within a minute.

Limit tokens are incrementally filled by 60(sec)/ rate limit. ex: 60(sec)/10(rate) gets rate token every 6 seconds up to max rate limit.

If you need to increase your rate limit, please log into your admin dashboard, find the app you would like a higher rate limit for, and click “request a higher rate limit". Please keep in mind that we require some form of working sample and/or an explanation of the need for a higher limit in order to approve rate limit increase requests.

The rate limit headers are defined as follows:

**X-RateLimit-Limit** - *Request limit per day / per minute*

**X-RateLimit-Remaining** - *The number of requests left for the time window*

**X-RateLimit-Reset** - *The remaining window before the rate limit is refilled in UTC epoch nanoseconds*



Expected Rate Limit Usage
-------------------------
Since the /matches and telemetry endpoints are not rate limited, the amount of rate limited requests a typical application needs to make to the API should be directly proportional to the number of users/players using it. For example, each time a player is looked up, the application needs to make two requests (if the information is not already cached):

- one to "/players?filter[playerNames]={playerName}" or "/players/{accountId} if the accountId is already known"
- one to "/players/{accountId}/seasons/{seasonId}" if season stats are required for the use case

**Any following requests to the /matches or telemetry endpoints will not count against the application's API key rate limit.**



Requesting a Higher Limit
-------------------------
If you find that the default (base tier) rate limit is not sufficient for your application, you can request a higher limit by selecting "I NEED A HIGHER LIMIT" in "MY APPS".

Please make sure that you fill out the form completely with as much detail as possible, and we will work with you to provide a more appropriate limit.

In order to determine an appropriate rate limit for your application, we need to know how many API requests your application makes, when it makes them, and analytics showing the number of users if you have active users. We will also want to know about the caching and optimization strategies you are using in order to help reduce the number of API requests that your application requires. Please take a look at our :ref:`Caching Overview` and :ref:`Caching Implementation` sections for additional information.

If your rate limit request is approved, you will receive a notice that a new API key has been created for you. You can find it under "MY APPS" where your old key used to be. Be sure to update your application with the new key within 24 hours before the old key is deactivated.
