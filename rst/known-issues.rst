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



Empty Participant stats
-----------------------
The following participant stats seem to always be 0:

- lastWinPoints
- mostDamage
- lastKillPoints



Missing LogItemDrop Events
--------------------------
LogItemDrop events are missing for attachments that are dropped at the same time as detaching them from a weapon. Attachments that are not attached to a weapon are logged normally when dropped.



[Xbox] Missing Attacker Info
-----------------------------
Attacker ID and location are always 0 in LogPlayerTakeDamage events.



[Xbox] Incorrect Kill Distance For Knocked Kills
-------------------------------------------------
killDistance is not always accurate for knocked kills.



[Xbox] Duplcate Attack IDs
--------------------------
Sometimes there are duplicate attackIds in a single telemetry file.
