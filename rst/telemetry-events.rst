.. _telemetry-events:

Telemetry Events
================

The following is a list of every telemetry event type with basic schemas to show the data that they contain. 

Data dictionaries and enums can be found  `here <https://github.com/pubg/api-assets>`_.

Objects shown as {object-name} are not described here in an effort to conserve space. More details about the objects in events can be located in the :ref:`telemetry-objects` reference. Please also note that each event contains the following fields which have been omitted from the outlines below::

  "_V": int,    // Version
  "_D": string, // Event timestamp
  "_T": string  // Event type

Telemetry associated with pc shards will also have the following fields in each event which have been omitted from the outlines below as well::

  "common": {Common} // PC only



LogPlayerLogin
--------------
.. code-block:: none

  "result":       bool,
  "errorMessage": string,
  "accountId":    string



LogPlayerCreate
---------------
.. code-block:: none

  "character": {Character}



LogPlayerPosition
-----------------
.. code-block:: none

  "character":       {Character},
  "elapsedTime":     number,
  "numAlivePlayers": int



LogPlayerAttack
---------------
.. code-block:: none

  "attackId":   int,
  "attacker":   {Character},
  "attackType": string,
  "weapon":     {Item},
  "vehicle":    {Vehicle}



LogItemPickup
-------------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogItemEquip
------------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogItemUnequip
--------------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogVehicleRide
--------------
.. code-block:: none

  "character": {Character},
  "vehicle":   {Vehicle},
  "seatIndex": int          // PC only



LogMatchDefinition
------------------
.. code-block:: none

  "MatchId":     string,
  "PingQuality": string



LogMatchStart
-------------
.. code-block:: none

  "mapName":               string,
  "weatherId":             string,
  "characters":            [{Character}, ...],
  "cameraViewBehaviour":   string,             
  "teamSize":              int,
  "isCustomGame":          bool,
  "isEventMode":           bool,                
  "blueZoneCustomOptions": string              

blueZoneCustomOptions is a stringified array of objects. See :ref:`blueZoneCustomOptions`.



LogGameStatePeriodic
--------------------
.. code-block:: none

  "gameState": {GameState}



LogVehicleLeave
---------------
.. code-block:: none

  "character":    {Character},
  "vehicle":      {Vehicle},
  "rideDistance": number,      // PC only
  "seatIndex":    integer      // PC only



LogPlayerTakeDamage
-------------------
.. code-block:: none

  "attackId":           int,
  "attacker":           {Character},
  "victim":             {Character},
  "damageTypeCategory": string,
  "damageReason":       string,
  "damage":             number,      // 1.0 damage = 1.0 health 
                                     // Net damage after armor; damage to health
  "damageCauserName":   string





LogPlayerLogout
---------------
.. code-block:: none

  "accountId": string



LogItemAttach
-------------
.. code-block:: none

  "character":  {Character},
  "parentItem": {Item},
  "childItem":  {Item}



LogItemDrop
-----------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogPlayerKill
-------------
.. code-block:: none

  "attackId":           int,
  "killer":             {Character},
  "victim":             {Character},
  "damageTypeCategory": string,
  "damageCauserName":   string,
  "damageReason":       string,
  "distance":           number



LogItemDetach
-------------
.. code-block:: none

  "character":  {Character},
  "parentItem": {Item},
  "childItem":  {Item}



LogItemUse
----------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogCarePackageSpawn
-------------------
.. code-block:: none

  "itemPackage": {ItemPackage}



LogVehicleDestroy
-----------------
.. code-block:: none

  "atackId":            int,
  "attacker":           {Character},
  "vehicle":            {Vehicle},
  "damageTypeCategory": string,
  "damageCauserName":   string,
  "distance":           number,



LogCarePackageLand
------------------
.. code-block:: none

  "itemPackage": {ItemPackage}



LogMatchEnd
-----------
.. code-block:: none

  "characters": [{Character}, ...]



LogSwimStart
------------
PC only

.. code-block:: none

  "character": {Character}


LogSwimEnd
----------
PC only

.. code-block:: none

  "character": {Character},
  "swimDistance": float



LogArmorDestroy
---------------
PC only

.. code-block:: none

  "attackId":           int,
  "attacker":           {Character},
  "victim":             {Character},
  "damageTypeCategory": string,
  "damageReason":       string,
  "damageCauserName":   string,
  "item":               {Item},
  "distance":           number



LogWheelDestroy
---------------
PC only

.. code-block:: none

  "attackId":           int,
  "attacker":           {Character},
  "vehicle":            {Vehicle},
  "damageTypeCategory": string,
  "damageCauserName":   string



LogPlayerMakeGroggy
-------------------
PC only

.. code-block:: none

  "attackId":            int,
  "attacker":            {Character},
  "victim":              {Character},
  "damageTypeCategory":  string,
  "damageCauserName":    string,
  "distance":            float,
  "isAttackerInVehicle": bool,
  "dBNOId":              int



LogPlayerRevive
---------------
PC only

.. code-block:: none

  "reviver":             {Character},
  "victim":              {Character}, // Yes, it's actually called victim
