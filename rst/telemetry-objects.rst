.. _telemetry-objects:

Telemetry Objects
=================

The following is a list of every telemetry object with basic schemas to show the data that they contain.

Data dictionaries and enums can be found  `here <https://github.com/pubg/api-assets>`_.



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



Common
------
.. code-block:: none

  {
    "isGame":  number
  },

isGame represents the phase of the game defined by the status of bluezone and safezone::

  isGame = 0 -> Before lift off
  isGame = 0.1 -> On airplane
  isGame = 0.5 -> When there’s no ‘zone’ on map(before game starts)
  isGame = 1.0 -> First safezone and bluezone appear
  isGame = 1.5 -> First bluezone shrinks
  isGame = 2.0 -> Second bluezone appears
  isGame = 2.5 -> Second bluezone shrinks
  ...



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



ItemPackage
-----------
.. code-block:: none

  {
    "itemPackageId": string,
    "location":      Location
    "items":         [{Item}, ...]
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



Vehicle
-------
.. code-block:: none

  {
    "vehicleType":   string,
    "vehicleId":     string,
    "healthPercent": number,
    "feulPercent":   number
  }