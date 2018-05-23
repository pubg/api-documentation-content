.. _telemetry-objects:

Telemetry Objects
=================

The following is a list of every telemetry object with basic schemas to show the data that they contain.

Data dictionaries and enums can be found  `here <https://github.com/pubg/api-assets>`_.



Common
------
.. code-block:: none

  {
    "matchId": string,
    "mapName": string,
    "isGame": float
  },



ItemPackage
-----------
.. code-block:: none

  {
    "itemPackageId": string,
    "location": Location
    "items": [{Item}, ...]
  }



Item
----
.. code-block:: none

  {
    "itemId": string,
    "stackCount": int,
    "category": string,
    "subCategory": string,
    "attachedItems": [ItemId, ...]
  }



Character
---------
.. code-block:: none

  {
    "name": string,
    "teamId": int,
    "health": float,
    "location": Location,
    "ranking": int,
    "accountId": string
  }



Vehicle
-------
.. code-block:: none

  {
    "vehicleType": string,
    "vehicleId": string,
    "healthPercent": float,
    "feulPercent": float
  }



GameState
---------
.. code-block:: none

  {
    "elapsedTime": int,
    "numAliveTeams": int,
    "numJoinPlayers": int,
    "numStartPlayers": int,
    "numAlivePlayers": int,
    "safetyZonePosition": Location,
    "safetyZoneRadius": float,
    "poisonGasWarningPosition": Location,
    "poisonGasWarningRadius": float,
    "redZonePosition": Location,
    "redZoneRadius": float
  }



.. _Location:

Location
--------
.. code-block:: none

  {
    "x": float,
    "y": float,
    "z": float
  }

- The range for the X and Y axes is 0 - 816,000 for 8km maps.
- Location values are measured in centimeters
