.. _getting-started:

Getting Started
===============
This guide will walk you through the basics of the PUBG API.

The URL
-------
When making a request to the PUBG API, the URL controls what data you will get back and how it will be displayed. Let's take a look at this example URL and break down the interesting bits::

  "https://api.pubg.com/shards/$platform/players?filter[playerNames]=$playerName"    

**shards/$platform** - *the platform shard*
    
- The PUBG API shards data by platform, and therefore requires a shard to be specified in the URL for most requests. In most cases, only the platform is required for the shard. However, the `platform-region` shard is required when making requests for PC and PS4 players' season stats for seasons prior to division.bro.official.2018-09, and for Xbox season stats for seasons before division.bro.official.2018-08. For more information about shards, please see :ref:`regions`

**players** - *the endpoint to query*

- Each endpoint provides different information relating to PUBG game data. More information about each available filter can be found within each endpoint documentation page.

**filter[playerNames]=$playerName** - *a filter specifying which players to search for*

- There are a variety of filters and options that can narrow down a search, organize results, and more! Additional information about each available filter can be found within each endpoint's documentation page.

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
We now have all of the pieces that we need to make our first request! Just make sure that you replace '$platform' and '$playerName' with your own information. Using CURL as an example, it will look like this::

  curl -g "https://api.pubg.com/shards/$platform/players?filter[playerNames]=$playerName" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

To see what the player response will look like, please head over to the :ref:`players` page.



Getting Match Lists For Players in Batches
------------------------------------------
You can get match lists for up to 10 players with one request like this::

  curl -g "https://api.pubg.com/shards/$platform/players?filter[playerNames]=$playerName-1,$playerName-2" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**filter[playerNames]=$playerName** - *a filter specifying which players to search for*

**Note: Use the platform shard when making requests for PC and PS4 players' season stats for seasons after division.bro.official.2018-09, and for Xbox season stats for seasons after division.bro.official.2018-08. Use the platform-region shard for making any other requests for players' season stats.**

Please be sure to replace '$platform' with the appropriate platform for the players that you are requesting information for. You can request information for up to 10 players by separating their account IDs with commas. This can also be done with in-game names rather than account IDs by changing ?filter[playerIds]' to '?filter[playerNames]' like this::

  curl -g "https://api.pubg.com/shards/$platform/players?filter[playerIds]=$playerId-1,$playerId-2" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**filter[playerIds]=$playerId** - *a filter specifying which player accounts to search for*

To see what the player response will look like, please head over to the :ref:`players` page.



Getting Player Season Stats
-----------------------------
The stats included in the participant objects within a match response show player stats in the context of that match, but it is also possible to obtain player stats for an entire season.

**Note: The list of seasons will only be changing about once every two months when a new seasons is added. Applications should not be querying for the list of seasons more than once per month.**

We start by querying the seasons endpoint to get a list of seasons like this. Please be sure to replace '$platform' with your own information::

  curl -g "https://api.pubg.com/shards/$platform/seasons" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

In the response you will see seasons listed like this::

  {
    "type": "season",
    "id": "$seasonId"
    "isCurrentSeason" true:
    "isOffseason": false:
  }

With this information, we can now query the API for season stats like this. Please be sure to replace '$platform', '$playerId', and '$seasonId' with you own information::

  curl -g "https://api.pubg.com/shards/$platform/players/$playerId/seasons/$seasonId"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**shards/$platform-region** - *the platform-region shard*

**filter[playerIds]=$playerId** - *a filter specifying which player accounts to search for*

**Note: Use the platform shard when making requests for PC and PS4 players' season stats for seasons after division.bro.official.2018-09, and for Xbox season stats for seasons after division.bro.official.2018-08. Use the platform-region shard for making any other requests for players' season stats.**

For more information about shards, please see :ref:`regions`

The match IDs for matches that count toward season stats will also be available. Custom matches and matches older than 14 days will not be available. Only the 32 most recent matches played within 14 days will be available.

To see what the season stats response will look like, please head over to the :ref:`seasons` page.



Getting Player Season Stats in Batches
--------------------------------------
You can get season stats for a game mode for up to 10 players with one request like this::

  curl -g "https://api.pubg.com/shards/$platform/seasons/$seasonId/gameMode/$gameMode/players?filter[playerIds]=$playerId-1,$playerId-2" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**shards/$platform-region** - *the platform-region shard*

**filter[playerIds]=$playerId** - *a filter specifying which player accounts to search for*

**gameMode/$gameMode** - *the game mode*

**Note: Use the platform shard when making requests for PC and PS4 players' season stats for seasons after division.bro.official.2018-09, and for Xbox season stats for seasons after division.bro.official.2018-08. Use the platform-region shard for making any other requests for players' season stats.**

Please be sure to replace '$platform', '$seasonId', and '$gameMode' with the appropriate platform, season ID, and game mode that you would like season stats for. You can request season stats for up to 10 players by separating their account IDs with commas.

To see what the season stats response will look like, please head over to the :ref:`seasons` page.



Getting Player Lifetime Stats
-----------------------------
Lifetime stats can be obtained for players by querying the seasons endpoint and using "lifetime" as the '$seasonId'. Please be sure to replace '$platform', and '$playerId' with your own information::

  curl -g "https://api.pubg.com/shards/$platform/players/$playerId/seasons/lifetime"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**filter[playerIds]=$playerId** - *a filter specifying which player accounts to search for*

**Note: The first seasons for lifetime stats are division.bro.official.pc-2018-01 for PC, division.bro.official.playstation-01 for PS4, and division.bro.official.xbox-01 for Xbox.**

To see what the lifetime stats response will look like, please head over to the :ref:`lifetime` page.



Getting Player Lifetime Stats in Batches
-----------------------------------------
You can get lifetime stats for a game mode for up to 10 players with one request. Please be sure to replace '$platform', and '$playerId' with your own information::

  curl -g "https://api.pubg.com/shards/$platform/seasons/lifetime/gameMode/$gameMode/players?filter[playerIds]=$playerId-1,$playerId-2" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**filter[playerIds]=$playerId** - *a filter specifying which player accounts to search for*

**gameMode/$gameMode** - *the game mode*

**Note: The first seasons for lifetime stats are division.bro.official.pc-2018-01 for PC, division.bro.official.playstation-01 for PS4, and division.bro.official.xbox-01 for Xbox.**

To see what the lifetime stats response will look like, please head over to the :ref:`lifetime` page.



Getting a Match
---------------
Within the response from the players endpoint, you should see a list of match IDs structured like this::

  "matches": {
    "data": [
      {
        "type": "match",
        "id": "matchId"
      }
    ]
  }

We can use this ID to retrieve the match from the matches endpoint like this. Please be sure the replace '$platform' and '$matchId' with your own information::

  curl -g "https://api.pubg.com/shards/$platform/matches/$matchId" \
  -H "Accept: application/vnd.api+json"

**Note: Make sure to use the tournament shard when getting tournament matches.**

**The data retention period is 14 days. Match data older than 14 days will not be available.**

To see what match responses look like, please head over to the :ref:`matches` page.



Getting Leaderboard Data
-------------------------
You can get the current leaderboard data for each game mode like this::

  curl -g "https://api.pubg.com/shards/$platform/leaderboards/$gameMode?page[number]=$page \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**$gameMode** - *the game mode*

**page[number]=$page** - *a filter specifying which page of the leaderboard to check*

Please be sure to replace '$platform' and '$gameMode' with the appropriate platform and game mode that you would like the leaderboard for. You will also need to specify which page of the leaderboard you would like by replacing '$page'. The leaderboard includes the top 1000 players for the specified game mode separated into 2 pages of 500 players each, numbered 0-1. The leaderboards will be updated every 2 hours.

To see what the leaderboards response will look like, please head over to the :ref:`leaderboards` page.



Getting Tournament Matches
--------------------------
Start by getting the list of tournaments to obtain the ID for the tournament you want to lookup like this::

  curl -g "https://api.pubg.com/tournaments" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

The response from the tournaments endpoint will contain an array of tournament references, showing their IDs and createdAt timestamps. Grab the ID of the desired tournament and use it to lookup the tournament like this. Be sure to replace '$tournamentId' with your own information::

  curl -g "https://api.pubg.com/tournaments/$tournamentId" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

**tournaments/$tournamentId** - *the tournament ID*

In response you will be given a list of match IDs from the tournament that you can lookup on the matches endpoint.

**Note: Be sure to use the tournament shard when looking up tournament matches.**

To see exactly what the tournament responses will look like, please head over to the :ref:`tournaments` page.



Getting Match Samples
---------------------
The samples endpoint offers a large set of random match references that is updated for each platform every 24 hours.

The number of matches per shard may vary. Requests for samples need to be at least 24hrs in the past UTC time using the filter[createdAt-start] query parameter. All matches in the response will be between the time that you choose and 24 hours earlier than that time. If you leave out this parameter, the response will be the most recent sample available (matches from within the last 24 hours).

A samples request looks like this. Please be sure to replace '$platform' and $startTime with your own information::

  curl -g "https://api.pubg.com/shards/$platform/samples?filter[createdAt-start]=$startTime" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

**shards/$platform** - *the platform shard*

**Note: Calling samples without filter[createdAt-start] will return the most recent samples list for that platform. You can fetch older samples up to 14 days using the filter.**

In the response, there will be an array of abbreviated match objects containing IDs and shards to look them up on the matches endpoint. This can be done as shown in the `Getting a Match`_ section.


Getting Telemetry Data
----------------------
Telemetry data will provide you with additional information for each match. This data is compressed using gzip and clients using the API should specify that they accept gzip compressed responses. The URL string that links to the telemetry file for a match can be found in the Asset Object of that match. For additional information, please refer to the :ref:`telemetry` page.
