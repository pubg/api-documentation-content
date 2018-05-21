.. _telemetry:

Telemetry
=========
Telemetry provides further insight into a match.

To retrieve Telemetry Data
---------------------------
You start by pulling a match from the matches endpoint. Remember to replace "some-region" and "matchId" with the appropriate region and matchId respectively.

Note: In order to get a match object, you will need to know its ID. You can find match IDs inside of player objects returned from the players endpoint. For more information about the players endpoint check out :ref:`players`. There is also a tutorial that may be helpful on the :ref:`getting-started` page.

.. code-block:: shell

  curl "https://api.playbattlegrounds.com/shards/some-region/matches/matchId" \
  -H "Accept: application/vnd.api+json"

You need to look for an assets reference in the match relationships object, which points to (contains the ID of) the full telemetry object within the included array. Check for the following in the response::

  "relationships": {
    ...
    "assets": {
      "data": [
        {
          "type": "asset",
          "id": "1ad97f85-cf9b-11e7-b84e-0a586460f004"
        }
      ]
    }
    ...
  }

Once you have located this ID, you now have to search for the object with that ID in the included array. The full object found there will provide you a link to the telemetry data, and look something like this::

  {
    "type": "asset",
    "id": "1ad97f85-cf9b-11e7-b84e-0a586460f004",
    "attributes": {
      "URL": "https://telemetry-cdn.playbattlegrounds.com/pc-krjp/2018/01/01/0/0/1ad97f85-cf9b-11e7-b84e-0a586460f004-telemetry.json", //Note this link will not work
      "createdAt": "2018-01-01T00:00:00Z",
      "description": "",
      "name": "telemetry"
    }
  },

You can download the data with following command. Please note that you do not need an API Key to get this data::

  curl "https://telemetry-cdn.playbattlegrounds.com/pc-krjp/2018/01/01/0/0/1ad97f85-cf9b-11e7-b84e-0a586460f004-telemetry.json" \
 	-H "Accept: application/vnd.api+json"

The telemetry file will contain an array of event objects, each with varying structure based on their type. For information about the included events, please see :ref:`telemetry-events`.
