.. _telemetry-objects:

Telemetry Objects
=================

The following is a list of every telemetry object with basic schemas to show the data that they contain.

.. role:: raw-html(raw)
   :format: html

Data dictionaries and enums can be found :raw-html:`<a class="tosAlert">here</a>`.


.. _blueZoneCustomOptions:

BlueZoneCustomOptions
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
    "name":         string,
    "teamId":       int,
    "health":       number,
    "location":     {Location},
    "ranking":      int,
    "accountId":    string
    "isInBlueZone": bool,
    "isInRedZone":  bool,
    "zone":         [regionId, ...]
  }



CharacterWrapper
----------------
.. code-block:: none

  {
    "character":           {Character},
    "primaryWeaponFirst":  string,
    "primaryWeaponSecond": string,
    "secondaryWeapon":     string,
    "spawnKitIndex":       int
  }



Common
------
.. code-block:: none

  {
    "isGame":  number
  }

isGame represents the phase of the game defined by the status of bluezone and safezone::

  isGame = 0 -> Before lift off
  isGame = 0.1 -> On airplane
  isGame = 0.5 -> When there’s no ‘zone’ on map(before game starts)
  isGame = 1.0 -> First safezone and bluezone appear
  isGame = 1.5 -> First bluezone shrinks
  isGame = 2.0 -> Second bluezone appears
  isGame = 2.5 -> Second bluezone shrinks
  ...



DamageInfo
----------
.. code-block:: none

  {
    "damageReason":             string,
    "damageTypeCategory":       string,
    "damageCauserName":         string,
    "additionalInfo":           [string, ...],
    "distance":                 number,
    "isThroughPenetrableWall":  bool
  }



GameResult
----------
.. code-block:: none

  {
    "rank":       int,
    "gameResult": string,
    "teamId":     int,
    "stats":      {Stats},
    "accountId":  string
  }



GameResultOnFinished
---------------------
.. code-block:: none

  {
    "results": [{GameResult}, ...]   // Shows winning players only
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
    "safetyZonePosition":       {Location},
    "safetyZoneRadius":         number,
    "poisonGasWarningPosition": {Location},
    "poisonGasWarningRadius":   number,
    "redZonePosition":          {Location},
    "redZoneRadius":            number,
    "blackZonePosition":        {Location},
    "blackZoneRadius":          number
  }



Item
----
.. code-block:: none

  {
    "itemId":        string,
    "stackCount":    int,
    "category":      string,
    "subCategory":   string,
    "attachedItems": [itemId, ...]
  }



ItemPackage
-----------
.. code-block:: none

  {
    "itemPackageId": string,
    "location":      {Location}
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

- Location values are measured in centimeters.
- (0,0) is at the top-left of each map.
- The range for the X and Y axes is 0 - 816,000 for Erangel, Miramar, Taego and Deston.
- The range for the X and Y axes is 0 - 612,000 for Vikendi.
- The range for the X and Y axes is 0 - 408,000 for Sanhok.
- The range for the X and Y axes is 0 - 306,000 for Paramo.
- The range for the X and Y axes is 0 - 204,000 for Karakin and Range.
- The range for the X and Y axes is 0 - 102,000 for Haven.



Stats
-----

.. code-block:: none

  {
    "killCount":           int,
    "distanceOnFoot":      number,
    "distanceOnSwim":      number,
    "distanceOnVehicle":   number,
    "distanceOnParachute": number,
    "distanceOnFreefall":  number
  }



Vehicle
-------
.. code-block:: none

  {
    "vehicleType":     string,
    "vehicleId":       string,
    "vehicleUniqueId": int,
    "healthPercent":   number,
    "feulPercent":     number,
    "altitudeAbs":     number,
    "altitudeRel":     number,
    "velocity":        number,
    "seatIndex":       int,
    "isWheelsInAir":   bool,
    "isInWaterVolume": bool,
    "isEngineOn":      bool
  }
