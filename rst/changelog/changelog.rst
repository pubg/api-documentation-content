.. _changelog:

Changelog
=========



Upcoming Changes
++++++++++++++++

No planned changes at the moment. To subscribe to our mailing list for changelog updates, `click here <http://eepurl.com/dFPTNL>`_.

.. To subscribe to our mailing list for changelog updates, `click here <http://eepurl.com/dFPTNL>`_.



v8.0.2
------

Bug Fixes:

- [PC] Fixed an issue where walkDistance, rideDistance, and swimDistance were all 0 for season stats.



v8.0.1
------

Bug Fixes:

- [PC] Fixed an issue where walkDistance, rideDistance, and swimDistance were all 0 for stats at the /matches endpoint.



v8.0.0
-------

Bug Fixes:

- [PC] Fixed an issue where attributes.shardId in the match object for tournaments was "steam" rather than "tournament".

New Data:

- The "tournament" shard is now available to use to get matches.

Deprecated:

- Using the platform-region shard at the /matches endpoint is deprecated.

Removed:

- [PC] LogMatchEnd.rewardDetail
- [PC] PlayTimeRecord
- [PC] RewardDetail



v7.8.0
-------

Bug Fixes:

- Fixed an issue where roster.attributes.won was sometimes false for the winning team.

New Data:

- [PC] playerSeason.attributes.gameModeStats.{gameMode}.rankPointsTitle
- [PC] GameResult
- [PC] PlayTimeRecord
- [PC] RewardDetail
- [PC] Stats
- [PC] LogHeal
- [PC] LogItemPickupFromCarePackage
- [PC] LogItemPickupFromLootbox
- [PC] LogObjectDestroy
- [PC] LogParachuteLanding
- [PC] LogRedZoneEnded
- [PC] LogVaultStart
- [PC] LogWeaponFireCount
- [PC] Character.isInBlueZone
- [PC] Character.isInRedZone
- [PC] Character.zone
- [PC] LogMatchEnd.rewardDetail
- [PC] LogSwimEnd.maxSwimDepthOfWater
- [PC] LogPlayerKill.assistant
- [PC] LogPlayerKill.damageCauserAdditionalInfo
- [PC] LogPlayerKill.dBNOId
- [PC] LogPlayerKill.victimGameResult
- [PC] LogPlayerMakeGroggy.damageCauserAdditionalInfo
- [PC] LogPlayerMakeGroggy.damageReason
- [PC] LogPlayerRevive.dBNOId
- [PC] LogVehicleLeave.maxSpeed



v7.7.0
------

Bug Fixes:

- [Xbox] Fixed an issue where attributes.isOffSeason would be "true" for an active season.

New Data:

- [PS4] The PS4 platform is supported.



v7.6.0
------

Bug Fixes:

- Fixed an issue where if there were two accounts with the same IGN, the most recent accountId was not returned for queries to the /players endpoint.

Deprecated:

- The platform-region shard is deprecated for the /players endpoint and the API will respond by returning data for all regions for the platform as if queried using the platform shard.



v7.5.0
------

Bug Fix:

- [PC] Fixed an issue where the timeSurvived and duration were sometimes a timestamp instead of seconds if a player logged out and then reconnected to the game before the match started.

New Data:

- [PC] The /leaderboards endpoint has been added and will return the top 100 players for each game mode.

Data Changes:

- The /players endpoint can now be queried by platform in addition to platform-region.



v7.4.0
------

Bug Fixes:

- [Xbox] Fixed an issue where there were sometimes duplicate attackIds within a single telemetry file
- [Xbox] Fixed an issue where the killDistance was not always accurate for knocked kills
- [Xbox] Health and location will now show values other than "0" for the attacker in LogPlayerTakeDamage events

New Data:

- Added LogPlayerPosition.vehicle



v7.3.0
------

New Data:

- [PC] Lifetime Stats as of division.bro.official.pc-2018-01 are available per gameMode by using "lifetime" as the seasonId at the /players/{accountId}/seasons/{seasonId} endpoint.



v7.2.0
------

Data Changes:

- [PC] playerSeason.attributes.gameModeStats.{gameMode}.rankPoints will be 0 when roundsPlayed < 10

Deprecated:

- [PC] participant.attributes.stats.rankPoints



v7.1.0
------

New Data:

- [PC] Added LogPlayerAttack.fireWeaponStackCount
- The /seasons endpoint can now be queried by platform in addition to platform-region



v7.0.0
------

New Data:

- [Xbox] New region xbox-sa has been added for South America
- status.data.type
- status.data.id

Removed:

- status.id
- status.attributes



v6.0.0
-------

New Data:

- [PC] participant.attributes.stats.rankPoints
- [PC] match.attributes.seasonState
- [PC] LogMatchDefinition.SeasonState
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.bestRankPoint
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.dailyWins
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.rankPoints
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.swimDistance
- [PC] playerSeason.attributes.gameModeStats.{gameMode}.weeklyWins

Data Changes:

- [PC] Matches and season stats from 10/3 onwards will be global and sharded by platform. PC Data prior to 10/3 and Xbox data will still be accessible with the old URL format.
- [PC] PC seasons after division.bro.official.2018-09 will be in the format division.bro.official.pc-{Year-Season number} rather than division.bro.official.{Year-Month}. The first season after division.bro.official.2018-09 is division.bro.official.pc-2018-01.

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

Bug Fixes:

- participant.attributes.stats.timeSurvived -- int -> number
- participant.attributes.stats.longestKill -- int -> number

Deprecated:

- player.attributes.createdAt
- player.attributes.updatedAt

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
