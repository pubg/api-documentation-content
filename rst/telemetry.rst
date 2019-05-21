.. _telemetry:

Telemetry
=========
Telemetry provides further insight into a match. This is where you will find the :ref:`telemetry-events` that occur throughout the match. In order to get the telemetry data, you will first need to get the link for it from within the match object. Detailed steps can be found below.

.. role:: raw-html(raw)
   :format: html

Data dictionaries and enums can be found :raw-html:`<a class="tosAlert">here</a>`.

To retrieve Telemetry Data
---------------------------
You will need to start by pulling a match from the matches endpoint. Remember to replace $platform and "matchId" with the appropriate platform and matchId respectively.

Note: In order to get a match object, you will need to know its ID. You can find match IDs inside of player objects returned from the players endpoint. For more information about the players endpoint check out :ref:`players`. There is also a tutorial that may be helpful on the :ref:`getting-started` page.

Your request should look something like the following:

.. code-block:: shell

  curl "https://api.pubg.com/shards/$platformn/matches/$matchId" \
  -H "Accept: application/vnd.api+json"

Next, you will need to find an "assets" reference in the match "relationships" object. This contains the ID of the full telemetry object. You will need this ID to locate the link for the telemetry file. Check for the following in the response::

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

Once you have located this ID, you can search for the telemetry object which has that ID in the included array. The full object found there will provide you with a link to the telemetry file, and look something like this::

  {
    "type": "asset",
    "id": "1ad97f85-cf9b-11e7-b84e-0a586460f004",
    "attributes": {
      "URL": "https://telemetry-cdn.pubg.com/pc-krjp/2018/01/01/0/0/1ad97f85-cf9b-11e7-b84e-0a586460f004-telemetry.json",
      "createdAt": "2018-01-01T00:00:00Z",
      "description": "",
      "name": "telemetry"
    }
  },

Now that you have the link to the telemetry file, you can download the data with the following command. Please note that you do not need an API Key to get this data::

  curl --compressed "https://telemetry-cdn.pubg.com/pc-krjp/2018/01/01/0/0/1ad97f85-cf9b-11e7-b84e-0a586460f004-telemetry.json" \
 	-H "Accept: application/vnd.api+json"

The telemetry file will contain an array of event objects, each with varying structure based on their type. For information about the included events, please see :ref:`telemetry-events`.

Note: Telemetry data is compressed using gzip. Many browsers and libraries support this without any extra work being necessary, but clients using the API should specify that they accept gzip compressed responses. Make sure that you pass the "Accept-Encoding: gzip" header.
