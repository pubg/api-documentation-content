.. _getting-started:

Getting Started
===============
This guide will walk you through the basics of the PUBG API

The URL
-------
When making a request to the PUBG API, the URL controls what data you will get back and how it will be displayed. Let's take a look at this example URL and break down the interesting bits::

  "https://api.pubg.com/shards/$platform-region-shard/players?filter[playerNames]=$player-name"    

**shards/$platform-region-shard** - *the platform region shard*
    
- The PUBG API shards data by platform and region, and therefore requires a shard to be specified in the URL for most requests. For more information about shards, please see :ref:`regions`

Note: Use the steam or kakao shard when making requests for PC players' season stats for seasons after and including division.bro.official.2018-01.

**players** - *the endpoint to query*

- Each endpoint provides different information relating to PUBG game data. More information about each available filter can be found within each endpoint documentation page.

**filter[playerNames]=$player-name** - *a filter specifying which players to search for*

- There are a variety of filters and options that can narrow down a search, organize results, and more! More information about each available filter can be found within each endpoint documentation page.

This URL will return a player object containing information about the requested player including a list of their recent match IDs. We will get into that more later in the tutorial.



Authorization
-------------
In order for the API to accept our request, we will need to send an API key via the `Authorization` header. More information about API keys can be found here: :ref:`api-keys`

The authorization string will look like this, where `$api-key` is your own personal API key::

  "Authorization: Bearer $api-key"



Content Negotiation
-------------------
Now we need to specify in the headers that we accept content in the format that the API returns. Clients using the API should specify that they accept responses using the `application/vnd.api+json` format. For convenience, we will also accept `application/json` since it is the default for many popular client libraries.

The content type string will look like this::

  "Accept: application/vnd.api+json"



Putting the Request Together
----------------------------
We now have all of the pieces that we need to make our first request! Just make sure that you replace '$platform-region-shard' and '$player-id' with your own information. Using CURL as an example, it will look like this::

  curl -g "https://api.pubg.com/shards/$platform-region-shard/players?filter[playerNames]=$player-id" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

To see what the player response will look like, please head over to the :ref:`players` page.



Getting Player Season Stats
-----------------------------
The stats included in the participant objects within a match response show player stats in the context of that match, but it is also possible to obtain player stats for an entire season.

We start by querying the seasons endpoint to get a list of seasons like this. Please be sure to replace '$platform-region-shard' with your own information::

  curl -g "https://api.pubg.com/shards/$platform-region-shard/seasons" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

Note: Use the steam or kakao shard when making requests for PC players' season stats for seasons after division.bro.official.2018-09. Seasons after division.bro.official.2018-09 will be in the format division.bro.official.{Year}-{Season number} rather than division.bro.official.{Year-Month}. The first season after division.bro.official.2018-09 is division.bro.official.2018-01.

In the response you will see seasons listed like this::

  {
    "type": "season",
    "id": "$season-name"
    "isCurrentSeason" true:
    "isOffseason": false:
  }

**Note: The list of seasons will only be changing about once per month when a new seasons is added. Applications should not be querying for the list of seasons more than once per month.**

With this information, we can now query the players endpoint like this. Please be sure to replace '$platform-region-shard', '$player-id', '$season-name', and with you own information::

  curl -g "https://api.pubg.com/shards/$platform-region-shard/players/$player-id/seasons/$season-name"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

To see what the season stats response will look like, please head over to the :ref:`seasons` page.



Getting a Match
---------------
Within the response from the players endpoint, you should see a list of match IDs structured like this::

  "matches": {
    "data": [
      {
        "type": "match",
        "id": "match-id"
      }
    ]
  }

We can use this ID to retrieve the match from the matches endpoint like this. Please be sure the replace '$platform-region-shard' and '$match-id' with your own information::

  curl -g "https://api.pubg.com/shards/$platform-region-shard/matches/$match-id" \
  -H "Accept: application/vnd.api+json"

Note: Make sure to use the pc-tournament shard when getting tournament matches.

To see what match response will look like, please head over to the :ref:`matches` page.



Getting Tournament Matches
--------------------------
Start by getting the list of tournaments to obtain the ID for the tournament you want to lookup like this::

  curl -g "https://api.pubg.com/tournaments" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

The response from the tournaments endpoint will contain an array of tournament references, showing their IDs and createdAt timestamps. Grab the ID of the desired tournament and use it to lookup the tournament like this. Be sure to replace '$tournament-id with your own information::

  curl -g "https://api.pubg.com/tournaments/$tournament-id" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

In response you will be given a list of match IDs that you can lookup on the matches endpoint.

Note: Be sure to use the pc-tournament shard when looking up tournament matches.

To see exactly what the tournament responses will look like, please head over to the :ref:`tournaments` page.



Getting Match Samples
---------------------
The samples endpoint offers a large set of random match references that is updated for each region every 24 hours.

A samples request looks like this. Please be sure to replace '$platform-region-shard' with your own information::

  curl -g "https://api.pubg.com/shards/$platform-region-shard/samples" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

Note: Calling samples without filter[createdAt-start] will return the most recent samples list for that region. You can fetch older samples up to 14 days using the filter.

In the response there will be an array of abbreviated match objects containing IDs and shards to look them up on the matches endpoint. This can be done as shown in the `Getting a Match`_ section.


Getting Telemetry Data
----------------------
Telemetry data will provide you with additional information for each match. This data is compressed using gzip and clients using the API should specify that they accept gzip compressed responses. The URL string that links to the telemetry file for a match can be found in the Asset Object of that match. For additional information, please refer to the :ref:`telemetry` page.
