.. _makingrequests:

Making Requests
===============

Content Negotiation
-------------------
Clients using the API should specify that they accept responses using the `application/vnd.api+json` format. For convenience, we will also accept `application/json` since it is the default for many popular client libraries.

The Server will respond with a `Content-Type` header that mirrors the format requested by the client.



Setting Headers
---------------
To specify the headers, use this code:

**Shell**

.. code-block:: shell

  curl "endpoint-url" \
  -H "Authorization: Bearer <api-key>"
  -H "Accept: application/vnd.api+json"

**Java**

.. code-block:: java

  import java.io.*;
  import java.net.*;

  URL url = new URL("endpoint-url");
  HttpURLConnection conn = (HttpURLConnection) url.openConnection();
  conn.setRequestMethod("GET");
  conn.setRequestProperty("Authorization","Bearer <api-key>");
  conn.setRequestProperty("Accept", "application/vnd.api+json");

  conn.getInputStream()

**Python**

.. code-block:: python

  import requests

  url = "endpoint-url"

  header = {
    "Authorization": "Bearer <api-key>",
    "Accept": "application/vnd.api+json"
  }

  r = requests.get(url, headers=header)

**Go**

.. code-block:: go

  import "net/http"

  client := &http.Client{}
  req, _ := http.NewRequest("GET","endpoint-url",nil)
  req.Header.Set("Authorization", "Bearer <api-key>")
  req.Header.Set("Accept", "application/vnd.api+json")
  res, _ := client.Do(req)



.. _parameters:

URL Parameters
---------------

.. _platform-shard:

the platform shard
........................................
**shards/$platform**

The PUBG API shards data by platform, and therefore requires a shard to be specified in the URL for most requests. In most cases, only the platform is required for the shard. However, the `platform-region` shard is required when making requests for PC and PS4 players' season stats for seasons prior to division.bro.official.2018-09, and for Xbox season stats for seasons before division.bro.official.2018-08. For more information about shards, please see :ref:`regions`.

.. _platform-region-shard:

the platform-region shard
..........................
**shards/$platform-region**

The platform-region shard should be used for making requests for season stats for seasons before the Survival Title system was launched:
  
- PC and PS4 season stats for seasons before and including division.bro.official.2018-09.
- Xbox season stats for seasons before and including division.bro.official.2018-08.

For more information about shards, please see :ref:`regions`.

Game Mode
..........
**gameMode/$gameMode**

Skip to :ref:`gamemodes` for more information about $gameMode values.

Match ID
.........
**matches/$matchId**

Match IDs are used to get match data and telemetry. They are listed within the responses from the players, samples, and season stats endpoints. Review :ref:`gettingMatch` for more information.

.. _seasonID:

Season ID
..........
**seasons/$seasonId**

Season IDs are used for :ref:`gettingSeasonStats`. They are available in responses from the :ref:`seasons` endpoint. Some stats are only available after the Survival Title system went live. For each platform, the first Survival Title season is:

- pc: division.bro.official.pc-2018-01
- psn: division.bro.official.playstation-01
- xbox: division.bro.official.xbox-01
- stadia: N/A, first season: division.bro.official.console-07

.. _lifetimeSeasonID:

Lifetime Season ID
...................
**seasons/lifetime**

The lifetime season ID can be used to get "lifetime" stats for a player. These are the same stats that are available in-game by choosing "Overall" while viewing your season stats. They include data beginning from when the Survival Title system was launched:

- PC lifetime stats begin with season division.bro.official.pc-2018-01
- Playstation lifetime stats begin with season division.bro.official.playstation-01
- Xbox lifetime stats begin with season division.bro.official.xbox-01
- Stadia lifetime stats begin with season division.bro.official.console-07

Player Account ID
......................
**players/$playerId**

Use this filter to specify which :ref:`player accounts<gettingPlayerId>` to search for.

Player Account IDs Filter
..........................
**filter[playerIds]=$playerId**

Use this filter to specify which player accounts to search for. You can search for up to 10 players at a time by separating their account IDs with commas.

Player Account Names Filter
............................
**filter[playerNames]=$playerName**

Use this filter to specify which players to search for. You can search for up to 10 players at a time by separating their player names (in-game names) with commas.

.. _gamepadFilter:

Gamepad Filter
...............
**filter[gamepad]=$isGamepad**

A filter specifying whether gamepad stats should be searched for instead of mouse/keyboard stats when using the `stadia` shard.

Stadia players have separate season stats for when they use a keyboard and mouse, and for when they use a gamepad. Gamepad stats can be queried for by using the `console` shard, or by using the gamepad filter with the `stadia` shard. When querying for these stats, $isGamepad should have the value `true`. This filter should be omitted otherwise. The API will respond with keyboard/mouse stats to queries for stats using the `stadia` shard without this filter.

Page Filter
...........
**page[number]=$page**

Leaderboards are separated into pages of 500 players each. Use the page filter to request additional pages. Pages are numbered beginning with 0. If this filter is omitted, the API will respond with the first page.


.. _regions:

Platforms and Regions
---------------------
The PUBG API shards data by either `platform` or `platform-region` depending on the request, and therefore requires a shard to be specified in the URL for most requests. The current shards are:

**shards/$platform** - *the platform shard*

- **kakao** - Kakao
- **stadia** - Stadia
- **steam** - Steam
- **tournament** - Tournaments
- **psn** - PS4
- **xbox** - Xbox
- **console** - PS4/Xbox (used for the /matches and /samples endpoints)

**shards/$platform-region** - *the platform-region shard*

- **pc-as** - Asia
- **pc-eu** - Europe
- **pc-jp** - Japan
- **pc-kakao** - Kakao
- **pc-krjp** - Korea
- **pc-na** - North America
- **pc-oc** - Oceania
- **pc-ru** - Russia
- **pc-sa** - South and Central America
- **pc-sea** - South East Asia
- **pc-tournament** - Tournaments
- **psn-as** - Asia
- **psn-eu** - Europe
- **psn-na** - North America
- **psn-oc** - Oceania
- **xbox-as** - Asia
- **xbox-eu** - Europe
- **xbox-na** - North America
- **xbox-oc** - Oceania
- **xbox-sa** - South America

The shard is specified after the pubg domain and before the endpoint like this::

  "...pubg.com/shards/steam/endpoint..."

**Note: Use the platform shard when making requests for Stadia players' season stats, PC and PS4 players' season stats for seasons after division.bro.official.2018-09, and for Xbox season stats for seasons after division.bro.official.2018-08. Use the platform-region shard for making any other requests for players' season stats.**

**The platform shard should be used at all other endpoints that require a shard. The platform-region shard is deprecated.**



.. _gamemodes:

Game Modes
----------
For some requests, a game mode is also required to be speicifed in the request URL. Valid game modes are:

- **solo** - 1 player per team, third person perspective
- **solo-fpp** - 1 player per team, first person perspective
- **duo** - up to 2 people per team, third person perspective
- **duo-fpp** - up to 2 people per team, first person perspective
- **squad** - more than 2 people per team, third person perspective
- **squad-fpp** - more than 2 people per team, first person perspective



GZIP
----
Clients can specify the header `Accept-Encoding: gzip`, and the server will compress responses. Responses will be returned with `Content-Encoding: gzip`.

Given the size of matches, this can have significant performance benefits.

To specify the header Accept-Encoding, use this code:

**Shell:**

.. code-block:: shell

  -H "Accept-Encoding: gzip"


**Java:**

.. code-block:: java

  conn.setRequestProperty("Accept-Encoding","gzip");


**Python:**

.. code-block:: python

  header = {"Accept-Encoding":"gzip"}


**Go:**

.. code-block:: go

  req.Header.Set("Accept-Encoding", "gzip")

Data Retention Period
---------------------
The data retention period is 14 days. **Match data** older than 14 days will not be available. Match lists go back 14 days for the players endpoint, and the season stats enpoint will show up to the 32 most recent matches within 14 days.



Responses
---------
All Server responses will be in JSON-API format and contain a root JSON object.

Each response will contain at least one of the following top-level members:

- `data` : the response's "primary data"
- `errors` : an array of error objects

A response may contain any of these top-level members:

- `links`: a links object related to the primary data.
- `included`: an array of resource objects that are related to the primary data and/or each other ("included resources").
- `meta`: not currently used.

If a document does not contain a top-level data key, the included array will not be present either.



Cross Origin Resource Sharing
-----------------------------
The API supports Cross Origin Resource Sharing (CORS) for AJAX requests from any origin. You can read the CORS W3C Recommendation `here <https://www.w3.org/TR/cors/>`_.

Here's a sample request sent from a browser hitting 'example.com':

**Shell:**

.. code-block:: shell

  curl -i https://api.pubg.com/status -H "Origin: http://example.com"
  HTTP/1.1 200 OK
  ...
  Access-Control-Allow-Origin: *
  Access-Control-Expose-Headers: Content-Length

This is what the CORS preflight request looks like:

.. code-block:: shell

  curl -i https://api.pubg.com/status -H "Origin: http://example.com" -X OPTIONS
  HTTP/1.1 200 OK
  ...
  Access-Control-Allow-Headers: Origin,X-Title-Id,Authorization
  Access-Control-Allow-Methods: GET,POST,OPTIONS
  Access-Control-Allow-Origin: *
  Access-Control-Max-Age: 86400
