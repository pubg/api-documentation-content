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



Missing LogItemDrop Events
--------------------------
LogItemDrop events are missing for attachments that are dropped at the same time as detaching them from a weapon. Attachments that are not attached to a weapon are logged normally when dropped.



Content Decoding Fails For Some Telemetry Files
-----------------------------------------------
Occassionally content decoding will fail for a telemetry file.



Missing Season Stats
---------------------
[PC] Data from seasons prior to division.bro.official.2018-04 is unavailable.
