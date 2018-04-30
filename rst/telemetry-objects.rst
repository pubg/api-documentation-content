.. _telemetry-objects:

Telemetry Objects
=================

The following is a list of every telemetry object with basic schemas to show the data that they contain.

Data dictionaries and enums can be found  `here <https://github.com/pubg/api-assets>`_.

**Note**: There is a difference between the key casing for pc and xbox telemetry. pc telemetry will have keys starting with a lowercase character, while xbox telemetry will have the same keys but starting with an uppercase character.

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
    "ItemPackageId": string,
    "Location": Location
    "Items": [{Item}, ...]
  }



Item
----
.. code-block:: none

  {
    "ItemId": string,
    "StackCount": int,
    "Category": string,
    "SubCategory": string,
    "AttachedItems": [ItemId, ...]
  }



Character
---------
.. code-block:: none

  {
    "Name": string,
    "TeamId": int,
    "Health": float,
    "Location": Location,
    "Ranking": int,
    "AccountId": string
  }



Vehicle
-------
.. code-block:: none

  {
    "VehicleType": string,
    "VehicleId": string,
    "HealthPercent": float,
    "FeulPercent": float
  }



GameState
---------
.. code-block:: none

  {
    "ElapsedTime": int,
    "NumAliveTeams": int,
    "NumJoinPlayers": int,
    "NumStartPlayers": int,
    "NumAlivePlayers": int,
    "SafetyZonePosition": Location,
    "SafetyZoneRadius": float,
    "PoisonGasWarningPosition": Location,
    "PoisonGasWarningRadius": float,
    "RedZonePosition": Location,
    "RedZoneRadius": float
  }



.. _Location:

Location
--------
.. code-block:: none

  {
    "X": float,
    "Y": float,
    "Z": float
  }

- The range for the X and Y axes is 0 - 816,000 for 8km maps.
- Location values are measured in centimeters
