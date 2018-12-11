.. _telemetry-events:

Telemetry Events
================

The following is a list of every telemetry event type with basic schemas to show the data that they contain. 

Data dictionaries and enums can be found  `here <https://github.com/pubg/api-assets>`_.

Objects shown as {object-name} are not described here in an effort to conserve space. More details about the objects in events can be located in the :ref:`telemetry-objects` reference. Please also note that each event contains the following fields which have been omitted from the outlines below::

  "_D": string,      // Event timestamp
  "_T": string,      // Event type
  "common": {Common}



LogArmorDestroy
---------------

.. code-block:: none

  "attackId":           int,
  "attacker":           {Character},
  "victim":             {Character},
  "damageTypeCategory": string,
  "damageReason":       string,
  "damageCauserName":   string,
  "item":               {Item},
  "distance":           number



LogCarePackageLand
------------------
.. code-block:: none

  "itemPackage": {ItemPackage}



LogCarePackageSpawn
-------------------
.. code-block:: none

  "itemPackage": {ItemPackage}



LogGameStatePeriodic
--------------------
.. code-block:: none

  "gameState": {GameState}



LogHeal
-------
[PC Only, Available Dec 19, 2018]

.. code-block:: none

  "character":  {Character},
  "item":       {Item},
  "healAmount": number



LogItemAttach
-------------
.. code-block:: none

  "character":  {Character},
  "parentItem": {Item},
  "childItem":  {Item}



LogItemDetach
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



LogItemEquip
------------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogItemPickup
-------------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogItemPickupFromCarePackage
----------------------------
[PC Only, Available Dec 19, 2018]

.. code-block:: none

  "character":   {Character},
  "item":        {Item}



LogItemPickupFromLootbox
------------------------
[PC Only, Available Dec 19, 2018]

.. code-block:: none

  "character":   {Character},
  "item":        {Item},
  "ownerTeamId": int



LogItemUnequip
--------------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogItemUse
----------
.. code-block:: none

  "character": {Character},
  "item":      {Item}



LogMatchDefinition
------------------
.. code-block:: none

  "MatchId":     string,
  "PingQuality": string,
  "SeasonState": string



LogMatchEnd
-----------
.. code-block:: none

  "characters":           [{Character}, ...],
  "gameResultOnFinished": {GameResultOnFinished},  // PC Only, Available Dec 19, 2018
  "rewardDetail":         [{RewardDetail}, ...]    // PC Only, Available Dec 19, 2018



LogMatchStart
-------------
.. code-block:: none

  "mapName":               string,
  "weatherId":             string,
  "characters":            [{Character}, ...],
  "cameraViewBehaviour":   string,             
  "teamSize":              int,
  "isCustomGame":          bool,
  "isEventMode":           bool,                // PC only    
  "blueZoneCustomOptions": string              

blueZoneCustomOptions is a stringified array of objects. See :ref:`blueZoneCustomOptions`.



LogObjectDestroy
----------------
[PC Only, Available Dec 19, 2018]

.. code-block:: none
  
  "character":      {Character},
  "objectType":     string,
  "objectLocation": {Location}



LogParachuteLanding
-------------------
[PC Only, Available Dec 19, 2018]

.. code-block:: none

  "character": {Character},
  "distance":  number



LogPlayerAttack
---------------
.. code-block:: none

  "attackId":             int,
  "fireWeaponStackCount": int,                // PC only
  "attacker":             {Character},
  "attackType":           string,
  "weapon":               {Item},
  "vehicle":              {Vehicle}



LogPlayerCreate
---------------
.. code-block:: none

  "character": {Character}



LogPlayerKill
-------------
.. code-block:: none

  "attackId":                   int,
  "killer":                     {Character},
  "victim":                     {Character},
  "assistant":                  {Character},  // PC Only, Available Dec 19, 2018
  "dBNOId":                     int           // PC Only, Available Dec 19, 2018
  "damageTypeCategory":         string,
  "damageCauserName":           string,
  "damageCauserAdditionalInfo": [string],     // PC Only, Available Dec 19, 2018
  "damageReason":               string,
  "distance":                   number,
  "victimGameResult":           {GameResult}   // PC Only, Available Dec 19, 2018



LogPlayerLogin
--------------
.. code-block:: none

  "accountId":    string



LogPlayerLogout
---------------
.. code-block:: none

  "accountId": string



LogPlayerMakeGroggy
-------------------

.. code-block:: none

  "attackId":                   int,
  "attacker":                   {Character},
  "victim":                     {Character},
  "damageReason":               string,       // PC Only, Available Dec 19, 2018
  "damageTypeCategory":         string,
  "damageCauserName":           string,
  "damageCauserAdditionalInfo": [string],     // PC Only, Available Dec 19, 2018
  "distance":                   number,
  "isAttackerInVehicle":        bool,
  "dBNOId":                     int



LogPlayerPosition
-----------------
.. code-block:: none

  "character":       {Character},
  "vehicle":         {Vehicle},
  "elapsedTime":     number,
  "numAlivePlayers": int



LogPlayerRevive
---------------

.. code-block:: none

  "reviver":             {Character},
  "victim":              {Character},
  "dBNOId":              int          // PC Only, Available Dec 19, 2018


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



LogRedZoneEnded
---------------
[PC Only, Available Dec 19, 2018]

.. code-block:: none

  "drivers": [{Character}, ...]



LogSwimEnd
----------

.. code-block:: none

  "character":           {Character},
  "swimDistance":        number,
  "maxSwimDepthOfWater": number  // PC Only, Available Dec 19, 2018



LogSwimStart
------------

.. code-block:: none

  "character": {Character}



LogVaultStart
-------------
[PC Only, Available Dec 19, 2018]

.. code-block:: none

  "character": {Character}



LogVehicleDestroy
-----------------
.. code-block:: none

  "atackId":            int,
  "attacker":           {Character},
  "vehicle":            {Vehicle},
  "damageTypeCategory": string,
  "damageCauserName":   string,
  "distance":           number,



LogVehicleLeave
---------------
.. code-block:: none

  "character":    {Character},
  "vehicle":      {Vehicle},
  "rideDistance": number,
  "seatIndex":    integer



LogVehicleRide
--------------
.. code-block:: none

  "character": {Character},
  "vehicle":   {Vehicle},
  "seatIndex": int,
  "maxSpeed":  number       // PC Only, Available Dec 19, 2018



LogWeaponFireCount
------------------
[PC Only, Available Dec 19, 2018]

.. code-block:: none

  "character": {Character},
  "weaponId":  string,
  "fireCount": int          // Increments of 10



LogWheelDestroy
---------------
.. code-block:: none

  "attackId":           int,
  "attacker":           {Character},
  "vehicle":            {Vehicle},
  "damageTypeCategory": string,
  "damageCauserName":   string
  