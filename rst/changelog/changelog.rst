.. _changelog:

Changelog
=========



Upcoming Changes
++++++++++++++++
.. No planned changes at the moment. To subscribe to our mailing list for changelog updates, `click here <http://eepurl.com/dFPTNL>`_.

v7.2.0 (planned for 10/19/18)
-----------------------------
Posted: 10/12/18

Deprecated:

- [PC] participant.attributes.stats.rankPoints

To subscribe to our mailing list for changelog updates, `click here <http://eepurl.com/dFPTNL>`_.



v7.1.0
------

New Data:

- [PC] Added LogPlayerAttack.fireWeaponStackCount
- The /seasons endpoint can now be queried by platform in addition to platform-region



v7.0.0
------

New Data:

- [Xbox] New region xbox-sa has been added for South America

Removed:

- status.id
- status.attributes

Added:

- status.data.type
- status.data.id

v6.0.0
-------

Data Changes:

- [PC] Matches and season stats from 10/3 onwards will be global and sharded by platform. PC Data prior to 10/3 and Xbox data will still be accessible with the old URL format.
- [PC] PC seasons after division.bro.official.2018-09 will be in the format division.bro.official.pc-{Year-Season number} rather than division.bro.official.{Year-Month}. The first season after division.bro.official.2018-09 is division.bro.official.pc-2018-01.

New Data:

- [PC] participant.attributes.stats.rankPoints
- [PC] match.attributes.seasonState
- [PC] LogMatchDefinition.SeasonState
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.bestRankPoint
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.dailyWins
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.rankPoints
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.swimDistance
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.weeklyWins

Deprecated:

- [PC] participant.attributes.stats.killPoints
- [PC] participant.attributes.stats.killPointsDelta
- [PC] participant.attributes.stats.winPoints
- [PC] participant.attributes.stats.winPointsDelta
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.killPoints
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.winPoints



v5.0.3
------

Bug Fix:

- The /players/{accountId}/seasons/{seasonId} endpoint will now return empty season stats if the player did not play during that season rather than a 404.



v5.0.2
------

Bug Fixes:

- [PC] Fixed an issue where there were sometimes duplicate attackIds within a single telemetry file
- [PC] Fixed an issue where the killDistance was not always accurate for knocked kills
- [PC] Health and location will now show values other than "0" for the attacker in LogPlayerTakeDamage events



v5.0.1
------

Bug Fix:

- The /players/{accountId}/seasons/{seasonId} endpoint will now return a 404 for season stats if the player did not play during that season.



v5.0.0
------

Data Changes:

- Squad size and perspective for custom matches will be added to attributes.gameMode in the Match object. Example: normal -> normal-squad-fpp



v4.0.0
------
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
