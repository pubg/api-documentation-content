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
    "isGame":  number
  },



ItemPackage
-----------
.. code-block:: none

  {
    "itemPackageId": string,
    "location":      Location
    "items":         [{Item}, ...]
  }



Item
----
.. code-block:: none

  {
    "itemId":        string,
    "stackCount":    int,
    "category":      string,
    "subCategory":   string,
    "attachedItems": [ItemId, ...]
  }



Character
---------
.. code-block:: none

  {
    "name":      string,
    "teamId":    int,
    "health":    number,
    "location":  Location,
    "ranking":   int,
    "accountId": string
  }



Vehicle
-------
.. code-block:: none

  {
    "vehicleType":   string,
    "vehicleId":     string,
    "healthPercent": number,
    "feulPercent":   number
  }



GameState
---------
.. code-block:: none

  {
    "elapsedTime":              int,
    "numAliveTeams":            int,
    "numJoinPlayers":           int,
    "numStartPlayers":          int,
    "numAlivePlayers":          int,
    "safetyZonePosition":       Location,
    "safetyZoneRadius":         number,
    "poisonGasWarningPosition": Location,
    "poisonGasWarningRadius":   number,
    "redZonePosition":          Location,
    "redZoneRadius":            number
  }



.. _Location:

Location
--------
.. code-block:: none

  {
    "x": number,
    "y": number,
    "z": number
  }

- The range for the X and Y axes is 0 - 816,000 for 8km maps.
- Location values are measured in centimeters



.. _blueZoneCustomOptions:

blueZoneCustomOptions
---------------------
The blueZoneCustomOptions string contains an array of config objects for each blue zone phase with the following structure::

  "phaseNum":                 int,
  "startDelay":               int,
  "warningDuration":          int,
  "releaseDuration":          int,
  "poisonGasDamagePerSecond": number,
  "radiusRate":               number,
  "spreadRatio":              number,
  "landRatio":                number,
  "circleAlgorithm":          int

The array of objects is stringified to look like this::

  "[{\"phaseNum\":0,\"startDelay\":120,\"warningDuration\":300,\"releaseDuration\":300,\"poisonGasDamagePerSecond\":0.40000000596046448,\"radiusRate\":0.34999999403953552,\"spreadRatio\":0.5,\"landRatio\":0.55000001192092896,\"circleAlgorithm\":0},...]"
