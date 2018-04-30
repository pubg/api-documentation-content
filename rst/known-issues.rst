.. _known-issues:

Known Issues
============
The following is a list of issues with the API that we are aware of. If you find a bug that isn't listed here, please report it using the "Report an API Bug" widget on the developer portal - |dev_portal_url|

**Note**: We will not be providing updates on these issues on this page. When fixed, they will be removed from this page and added to the changelog.

Mispellings
-----------
The following items are misspelled in the telemetry:

- Item.ItemID: Cowbar_C
- Item.ItemID: ItemAmmo12GuageC
- Vehicle.FeulPercent



Inconsistent Casing
-------------------
XBOX and PC telemetry have different casing for the first letter of each key in the telemetry.



Inconsistent Time Zones
-----------------------
LogMatchDefinition events have a different format for their timestamp. It appears as 2018-04-05T22:17:38.0817861+00:00" as opposed to "2018-04-05T22:16:10.064Z" for other events.



Missing Attacker Info
---------------------
Attacker ID and location are always 0 in LogPlayerTakeDamage events.



Duplicate Ranks
---------------
Sometimes multiple rosters in a match have the same rank.



Empty Participant stats
-----------------------
The following participant stats seem to always be 0:

- lastWinPoints
- mostDamage
- WeaponsAcquired
- lastKillPoints
- killStreaks



Delayed Xbox matches
--------------------
Xbox matches take significantly longer than PC to become available through the API.
