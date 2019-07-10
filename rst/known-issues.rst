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



Inaccurate Values for bestRankPoint
------------------------------------
bestRankPoint in the game mode stats object is the highest value achieved for rankPoints during the season across all game modes. Since the values are only updated for each game mode after that game mode has been played, the value of bestRankPoint is not always up to date across all game modes.



Missing Log Events for Throwable Items
---------------------------------------
The number of grenades and smoke bombs dropped may sometimes exceed the number of items that have been picked up.
