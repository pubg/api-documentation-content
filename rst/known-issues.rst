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



Missing Season Stats
---------------------
[PC] Data from seasons prior to division.bro.official.2018-04 is unavailable.



Missing Log Events for Throwable Items
---------------------------------------
The number of grenades and smoke bombs dropped may sometimes exceed the number of items that have been picked up.



Inaccurate Values for "assists" in the participant object
----------------------------------------------------------
Players may sometimes have a different number of assists in participant.attributes.stats than represented by the log events in the telemetry file for a match.



Inaccurate Values for "headshotKills" in the participant object
----------------------------------------------------------------
Players may sometimes have a different number of headshotKills in participant.attributes.stats than LogPlayerKill events with damageReason of "HeadShot". In these cases, the headshotkills are often awarded to the attacker that knocked the victim instead of the killer.



Inaccurate Values for "roadKills" in the participant object
------------------------------------------------------------
Players may sometimes have a different number of roadKills in participant.attributes.stats than LogPlayerKill events with damageTypeCategory of "Damage_VehicleHit".



Inaccurate Values for "fireWeaponStackCount" in LogPlayerAttack
---------------------------------------------------------------
The values for LogPlayerAttack.fireWeaponStackCount are sometimes inaccurate. In these cases, the values are often at least several thousand.



victim.location for LogPlayerTakeDamage and LogPlayerKill events are sometimes 0
----------------------------------------------------------------------------------
The values for LogPlayerTakeDamage.victim.location and LogPlayerKill.victim.location may be 0 when damageTypeCategory is "Damage_Groggy".



Item_Weapon_vz61Skorpion_C and Item_Weapon_FlareGun_C are listed with the subCategory "Main"
---------------------------------------------------------------------------------------------
Item_Weapon_vz61Skorpion_C and Item_Weapon_FlareGun_C are listed in the telemetry with the subCategory "Main" instead of "Handgun" for log events.
