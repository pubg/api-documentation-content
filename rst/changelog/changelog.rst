.. _changelog:

Changelog
=========

Upcoming Changes
----------------
.. No planned changes at the moment.

v4.0.0 (planned for 8/8/18)
+++++++++++++++++++++++++++
Posted: 7/11/18

Data Changes:

- Telemetry data will be compressed using gzip



v3.2.0
------
New Data:

- [Xbox] Common
- [Xbox] LogPlayerKill.damageReason
- [Xbox] LogSwimEnd.swimDistance
- [Xbox] LogWheelDestroy



v3.1.0
------
New Data:

- Tournaments endpoint and matches



v3.0.0
------
Data Changes:

- Empty attacker objects in LogPlayerTakeDamage events will be null instead of empty
- Empty vehicle objects in LogPlayerAttack will be null instead of empty



v2.0.0
------
Deprecated:

- player.attributes.createdAt
- player.attributes.updatedAt

Bug Fixes:

- participant.attributes.stats.timeSurvived -- int -> number
- participant.attributes.stats.longestKill -- int -> number

Removed:

- (any).common.mapName //available in LogMatchStart
- (any).common.matchId //available in LogMatchDefinition
- (any)._V
- LogPlayerLogin.errorMessage
- LogPlayerLogin.result



v1.4.0
------
New Data:

- LogPlayerMakeGroggy
- LogPlayerRevive

- [PC] LogWheelDestroy
- [PC] LogSwimEnd.swimDistance
- [PC] LogPlayerKill.damageReason
- [PC] LogMatchStart.isCustomGame
- [PC] LogMatchStart.isEventMode



v1.3.1
------
Bug Fixes:

- Rosters will show highest participant rank
- Existing player's that haven't played in 7 days will no longer return a 404 not found error



v1.3.0
------
New Data:

- Custom match data
- Added isCustomMatch boolean flag to match.attributes

- [Xbox] added swimDistance to participant.attributes.stats (will appear for Xbox, but will always be 0)
- [Xbox] added LogSwimStart and LogSwimEnd telemetry events
- [Xbox] added LogArmorDestroy telemetry events
- [Xbox] added rideDistance and seatIndex fields to LogVehicleLeave telemetry events
- [Xbox] added seatIndex to LogVehicleRide telemetry events



v1.2.0
------
New Data:

- [PC] added swimDistance to participant.attributes.stats (will appear for Xbox, but will always be 0)
- [PC] added LogSwimStart and LogSwimEnd telemetry events
- [PC] added LogArmorDestroy telemetry events
- [PC] added rideDistance and seatIndex fields to LogVehicleLeave telemetry events
- [PC] added seatIndex to LogVehicleRide telemetry events



v1.1.1
------
Bug fixes:

- participant.attributes.stats.killStreaks is now populated correctly
- participant.attributes.stats.weaponsAcquired is now populated correctly



v1.1.0
------
Bug fixes:

- [Xbox] keys in the telemetry data are now lowercase
- [Xbox] Matches are no longer delayed compared to PC matches

New Data:

- [Xbox] mapName will now be included in match records
