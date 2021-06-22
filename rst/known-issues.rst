.. _known-issues:

Known Issues
============
The following is a list of issues with the API that we are aware of. If you find a bug that isn't listed here, please report it by sending an email to pubgapi@pubg.com.

**Note**: We will not be providing updates on these issues on this page. When fixed, they will be removed from this page and added to the changelog.

Mispellings
-----------
The following items are misspelled in the telemetry:

- Item.ItemID: Cowbar_C
- Item.ItemID: ItemAmmo12GuageC
- Vehicle.FeulPercent
- ItemPackage.itemPackageId.Carapackage_RedBox_C
- damageReason.SimlateAIBeKilled



Missing Season Stats
---------------------
[PC] Data from seasons prior to division.bro.official.2018-04 is unavailable.



Missing Log Events for Throwable Items
---------------------------------------
The number of grenades and smoke bombs dropped may sometimes exceed the number of items that have been picked up.



victim.location for LogPlayerTakeDamage events are sometimes 0
---------------------------------------------------------------
The values for LogPlayerTakeDamage.victim.location may be 0 when damageTypeCategory is "Damage_Groggy".



Item_Weapon_vz61Skorpion_C and Item_Weapon_FlareGun_C are listed with the subCategory "Main"
---------------------------------------------------------------------------------------------
Item_Weapon_vz61Skorpion_C and Item_Weapon_FlareGun_C are listed in the telemetry with the subCategory "Main" instead of "Handgun" for log events.



Inaccurate Values for "swimDistance", "rideDistance", and "walkDistance" in the participant object
---------------------------------------------------------------------------------------------------
Players may sometimes have different values for distances in participant.attributes.stats than in the GameResult object. In this case, GameResult should be considered as having the accurate values. The GameResult object can be found in LogPlayerKillV2.victimGameResult and LogMatchEnd.results.gameResultOnFinished.
