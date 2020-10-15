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

- There are a variety of filters and options that can narrow down a search, organize results, and more! Additional information about each available filter can be found in :ref:`parameters`, and within each endpoint's documentation page.

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


.. _firstRequest:

Putting the Request Together
----------------------------
We now have all of the pieces that we need to make our first request! Just make sure that you replace '$platform' and '$playerName' with your own information. Using CURL as an example, it will look like this::

  curl -g "https://api.pubg.com/shards/$platform/players?filter[playerNames]=$playerName" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

To see what the player response will look like, please head over to the :ref:`players` page.


.. _gettingPlayerId:

Finding the Player Account ID
------------------------------
Players' account IDs are available in the response from :ref:`firstRequest`. In the response you will see players listed like this::

  {
    "type": "player",
    "id": "$playerId"
  }



Ranked, Season, and Lifetime Stats
-----------------------------------
The stats included in the participant objects within a match response show player stats in the context of that match, but it is also possible to obtain player stats for an entire season or their overall stats. You will need a **playerId** and a **seasonId** to get ranked, season, or lifetime stats.

The :ref:`lifetimeSeasonID` can be used to get "lifetime" stats for a player. These are the same stats that are available in-game by choosing "Overall" while viewing your season stats. They include data beginning from when the Survival Title system was launched. The first seasons for lifetime stats are `division.bro.official.pc-2018-01` for PC, `division.bro.official.playstation-01` for PS4, `division.bro.official.xbox-01` for Xbox, and `division.bro.official.console-07` for Stadia.

Stadia players have separate season and lifetime stats for when they use a keyboard and mouse, and for when they use a gamepad. Gamepad stats can be queried for by using the `console` shard, or by using the :ref:`gamepadFilter` with the `stadia` shard.

We start by querying the seasons endpoint to get a list of seasons:


Getting Season IDs
...................
Query the seasons endpoint to get a list of seasons like this. Please be sure to replace '$platform' with your own information::

  curl -g "https://api.pubg.com/shards/$platform/seasons" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

**Note: The list of seasons will only be changing about once every two months when a new seasons is added. Applications should not be querying for the list of seasons more than once per month.**

In the response you will see seasons listed like this::

  {
    "type": "season",
    "id": "$seasonId",
    "attributes": {
      "isCurrentSeason": true,
      "isOffseason": false
    }
  }

To see what the full seasons response will look like, please head over to the :ref:`seasons` page.



.. _gettingSeasonStats:

Getting Player Season Stats
............................
Now that we know the $seasonId, we can query the API for season stats like this. Please be sure to replace '$platform', '$playerId', and '$seasonId' with you own information::

  curl -g "https://api.pubg.com/shards/$platform/players/$playerId/seasons/$seasonId"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

You will need to use the :ref:`platform-region-shard` when making requests for stats from seasons that occurred before the Survial Title system was introduced.

Match IDs for matches that were played within 14 days will also be available. A maximum of 32 match IDs per player will be in the response. Custom matches and matches older than 14 days will not be available.

To see what the season stats response will look like, please head over to the :ref:`seasons` page.



.. _gettingRankedStats:

Getting Player Ranked Stats
............................
Ranked stats are available beginning with Season 7. We can query the API for ranked stats by adding `/ranked` to the request URL for season stats::

  curl -g "https://api.pubg.com/shards/$platform/players/$playerId/seasons/$seasonId/ranked"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

A list of match IDs is not available from this endpoint. To see what the ranked stats response will look like, please head over to the :ref:`seasons` page.



Getting Player Lifetime Stats
..............................
Lifetime stats are the stats that are available in-game by choosing "Overall" while viewing your season stats. They can be obtained for players by querying the seasons endpoint and using "lifetime" as the '$seasonId'::

  curl -g "https://api.pubg.com/shards/$platform/players/$playerId/seasons/lifetime"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

The first season included in lifetime stats for each platform is listed in :ref:`lifetimeSeasonID`. To see what the lifetime stats response will look like, please head over to the :ref:`lifetime` page.



Making Batch Requests
----------------------
You can make requests for season/lifetime stats and for players in batches of up to 10 players at a time. This should be done whenever possible to help reduce the number of rate-limited requests that are required by your application.



Making Batch Requests For Stats
................................
You can get season stats for a single game mode for up to 10 players at a time like this::

  curl -g "https://api.pubg.com/shards/$platform/seasons/$seasonId/gameMode/$gameMode/players?filter[playerIds]=$playerId-1,$playerId-2" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

You will need to use the :ref:`platform-region-shard` when making requests for stats from seasons that occurred before the Survial Title system was introduced.

To see what the season stats response will look like, please head over to the :ref:`seasons` page.

Lifetime stats for a single game mode can also be requested for up to 10 players at a time by using "lifetime" as the `$seasonId`::

  curl -g "https://api.pubg.com/shards/$platform/seasons/lifetime/gameMode/$gameMode/players?filter[playerIds]=$playerId-1,$playerId-2" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

To see what the lifetime stats response will look like, please head over to the :ref:`lifetime` page.



Getting Match Lists For Players in Batches
...........................................
You can get match lists for up to 10 players with one request like this::

  curl -g "https://api.pubg.com/shards/$platform/players?filter[playerNames]=$playerName-1,$playerName-2" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

Please be sure to replace '$platform' with the appropriate platform for the players that you are requesting information for. You can request information for up to 10 players by separating their account IDs with commas. This can also be done with in-game names rather than account IDs by changing ?filter[playerIds]' to '?filter[playerNames]' like this::

  curl -g "https://api.pubg.com/shards/$platform/players?filter[playerIds]=$playerId-1,$playerId-2" \
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

To see what the player response will look like, please head over to the :ref:`players` page.



.. _gettingMatch:

Getting a Match
----------------
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



Getting Match Samples
---------------------
The samples endpoint offers a large set of random match references that is updated for each platform every 24 hours. Sample rates are independent for each platform and not uniform across any time interval. They cannot and should not be used to attempt to estimate the total number of matches or unique PUBG players, or as a way to compare the number of matches or unique PUBG players per platform.

The number of matches per shard may vary. Requests for samples need to be at least 24hrs in the past UTC time using the filter[createdAt-start] query parameter. All matches in the response will be between the time that you choose and 24 hours earlier than that time. If you leave out this parameter, the response will be the most recent sample available (matches from within the last 24 hours).

A samples request looks like this. Please be sure to replace '$platform' and $startTime with your own information::

  curl -g "https://api.pubg.com/shards/$platform/samples?filter[createdAt-start]=$startTime" \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

**Note: Calling samples without filter[createdAt-start] will return the most recent samples list for that platform. You can fetch older samples up to 14 days using the filter.**

In the response, there will be an array of abbreviated match objects containing IDs and shards to look them up on the matches endpoint. This can be done as shown in the `Getting a Match`_ section.



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



Getting Telemetry Data
----------------------
Telemetry data will provide you with additional information for each match. This data is compressed using gzip and clients using the API should specify that they accept gzip compressed responses. The URL string that links to the telemetry file for a match can be found in the Asset Object of that match. For additional information, please refer to the :ref:`telemetry` page.



Getting Player Mastery Stats
-----------------------------
Weapon Mastery and Survival Mastery information can be obtained for players by querying the weapon_mastery and survival_mastery endpoints. Don't forget to replace '$platform', and '$playerId' with your own information.

Weapon Mastery::

  curl -g "https://api.pubg.com/shards/$platform/players/$playerId/weapon_mastery"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

Survival Mastery::

  curl -g "https://api.pubg.com/shards/$platform/players/$playerId/survival_mastery"
  -H "Authorization: Bearer $api-key" \
  -H "Accept: application/vnd.api+json"

You can see what the responses will look like at the :ref:`mastery` page.



Getting Leaderboard Data
-------------------------
Leaderboards are available for each season beginning with the first Survival Title :ref:`seasonID` for each platform. Each leaderboard includes the top 500 players for the specified game mode. Leaderboards for the current season will be updated every 2 hours. :ref:`platform-region-shard` shard should be used to get leaderboards beginning with season division.bro.official.pc-2018-07 (for PC) and season division.bro.official.console-07 (for console). :ref:`platform-shard` is only supported up to Season 6.

You can get the current leaderboard data for each game mode like this::

  curl -g "https://api.pubg.com/shards/$platform-region/leaderboards/$seasonId/$gameMode \
  -H "Authorization: Bearer api-key" \
  -H "Accept: application/vnd.api+json"

Please be sure to replace '$platform-region', '$seasonId', and '$gameMode' with the appropriate platform, season ID, and game mode that you would like the leaderboard for. Refer to `Getting Player Season Stats`_ for information about how to get season IDs. You will also need to specify which page of the leaderboard you would like by replacing '$page'.

To see what the leaderboards response will look like, please head over to the :ref:`leaderboards` page.
