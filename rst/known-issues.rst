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


Missing LogItemDrop Events
--------------------------
LogItemDrop events are missing for attachments that are dropped at the same time as detaching them from a weapon. Attachments that are not attached to a weapon are logged normally when dropped.



Missing Season Stats
---------------------
[PC] Data from seasons prior to division.bro.official.2018-04 is unavailable.



Content Decoding Fails For Some Telemetry Files
-----------------------------------------------
Occassionally content decoding will fail for a telemetry file.



Incorrect attributes for matches at the /tournaments endpoint
-------------------------------------------------------------
attributes.isCustomMatch is false and attributes.gameMode is "normal" in the match object for most matches at the /tournaments endpoint.
