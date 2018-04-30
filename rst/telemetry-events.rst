.. _telemetry-events:

Telemetry Events
================

The following is a list of every telemetry event type with basic schemas to show the data that they contain. 

Data dictionaries and enums can be found  `here <https://github.com/pubg/api-assets>`_.

Objects shown as {object-name} are not described here in an effort to conserve space. More details about the objects in events can be located in the :ref:`telemetry-objects` reference. Please also note that each event contains the following fields which have been omitted from the outlines below::

  "_V" - Version
  "_D" - Event timestamp
  "_T" - Event type

Telemetry associated with pc shards will also have the following fields in each event which have been omitted from the outlines below as well::

  "Common": {Common} //Only for PC telemetry

In addition, there is a difference between the key casing for pc and xbox telemetry. pc telemetry will have keys starting with a lowercase character, while xbox telemetry will have the same keys but starting with an uppercase character.



LogPlayerLogin
--------------
.. code-block:: none

  "Result": bool,
  "ErrorMessage": string,
  "AccountId": string



LogPlayerCreate
---------------
.. code-block:: none

  "Character": {Character}



LogPlayerPosition
-----------------
.. code-block:: none

  "Character": {Character},
  "ElapsedTime": float,
  "NumAlivePlayers": int



LogPlayerAttack
---------------
.. code-block:: none

  "AttackId": int,
  "Attacker": {Character},
  "AttackType": string,
  "Weapon": {Item},
  "Vehicle": {Vehicle}



LogItemPickup
-------------
.. code-block:: none

  "Character": {Character},
  "Item": {Item}



LogItemEquip
------------
.. code-block:: none

  "Character": {Character},
  "Item": {Item}



LogItemUnequip
--------------
.. code-block:: none

  "Character": {Character},
  "Item": {Item}



LogVehicleRide
--------------
.. code-block:: none

  "Character": {Character},
  "Vehicle": {Vehicle}



LogMatchDefinition
------------------
.. code-block:: none

  "MatchId": string,
  "PingQuality": string //Only for PC telemetry



LogMatchStart
-------------
.. code-block:: none

  "Characters": [{Character}, ...]



LogGameStatePeriodic
--------------------
.. code-block:: none

  "GameState": {GameState}



LogVehicleLeave
---------------
.. code-block:: none

  "Character": {Character},
  "Vehicle": {Vehicle}



LogPlayerTakeDamage
-------------------
.. code-block:: none

  "AttackId": int,
  "Attacker": {Character},
  "Victim": {Character},
  "DamageTypeCategory": string,
  "DamageReason": string,
  "Damage": float,
  "DamageCauserName": string



LogPlayerLogout
---------------
.. code-block:: none

  "AccountId": string



LogItemAttach
-------------
.. code-block:: none

  "Character": {Character},
  "ParentItem": {Item},
  "ChildItem": {Item}



LogItemDrop
-----------
.. code-block:: none

  "Character": {Character},
  "Item": {Item}



LogPlayerKill
-------------
.. code-block:: none

  "AttackId": int,
  "Killer": {Character},
  "Victim": {Character},
  "DamageTypeCategory": string,
  "DamageCauserName": string,
  "Distance": float



LogItemDetach
-------------
.. code-block:: none

  "Character": {Character},
  "ParentItem": {Item},
  "ChildItem": {Item}



LogItemUse
----------
.. code-block:: none

  "Character": {Character},
  "Item": {Item}



LogCarePackageSpawn
-------------------
.. code-block:: none

  "ItemPackage": {ItemPackage}



LogVehicleDestroy
-----------------
.. code-block:: none

  "AttackId": int,
  "Attacker": {Character},
  "Vehicle": {Vehicle},
  "DamageTypeCategory": string,
  "DamageCauserName": string,
  "Distance": float,



LogCarePackageLand
------------------
.. code-block:: none

  "ItemPackage": {ItemPackage}



LogMatchEnd
-----------
.. code-block:: none

  "Characters": [{Character}, ...]
