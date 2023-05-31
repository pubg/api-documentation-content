.. _changelog:

Changelog
=========



Upcoming Changes
-----------------

No planned changes at the moment.

v22.0.2
-------

New Data:

- Add tier to survival mastery object



v22.0.1
-------

New Data:

- Add ban type to player object



v22.0.0
-------

New Data:

- [PC, Console] weaponMasterySummary.weaponSummaries.{Item_Weapon}.OfficialStatsTotal has been added to Weapon Mastery beginning with the 18.2 patch. These stats will not include previous Weapon Mastery stats.
- weaponMasterySummary.weaponSummaries.{Item_Weapon}.CompetitiveStatsTotal has been added to Weapon Mastery beginning with the 18.2 patch. These stats will not include previous Weapon Mastery stats.

Data Changes:

- Weapon Mastery stats prior to the 18.2 patch will still be shown in weaponMasterySummary.weaponSummaries.{Item_Weapon}.StatsTotal, but they will no longer be updated.

Deprecated:

- weaponMasterySummary.weaponSummaries.{Item_Weapon}.Medals



v21.3.0
--------

New Data:

- LogCharacterCarry



v21.2.0
--------

New Data:

- LogItemPutToVehicleTrunk
- LogItemPickupFromVehicleTrunk
- New attributes.matchType enums: "airoyale", "seasonal"



v21.1.0
--------

New Data:

- LogPlayerRedeploy
- LogPlayerRedeployBRStart



v21.0.0
--------

Removed:

- [PC, Console] LogPlayerKill

LogPlayerKill events will not be removed from matches that finished before this update. This update does not effect tournament matches.

Bug Fix:

- Fixed the issue where players would sometimes have a different number of assists in participant.attributes.stats than indicated by the log events in the telemetry file for a match.



v20.5.0
--------

New Data:

- LogPlayerDestroyProp
- LogPlayerKillV2.assists_AccountId
- LogPlayerKillV2.teamKillers_AccountId



v20.4.0
--------

New Data:

- LogEmPickupLiftOff



v20.3.0
--------

New Data:

- LogPlayerKillV2

Bug Fix:

- Fixed the issue where the value for participant.attributes.stats.killStreaks was always 0.



v20.2.0
--------

New Data:

- LogItemPickupFromCustomPackage
- LogVehicleDamage
- The Survival Mastery endpoint is available.

Bug Fix:

- Fixed unexpected data for deprecated Player.attributes.createdAt and Player.attributes.updatedAt



v20.1.0
--------

Deprecated:

- leaderboard.included.player.attributes.stats.winRatio
- leaderboard.included.player.attributes.stats.killDeathRatio
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.reviveRatio
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.revives
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.heals
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.boosts
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.weaponsAcquired
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.teamKills
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.playTime
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.killStreak
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.avgSurvivalTime
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.kdr
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.roundMostKills
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.longestKill
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.headshotKills
- rankedplayerstats.attributes.rankedGameModeStats.{gameMode}.headshotKillRatio



v20.0.0
--------

New Data:

- Player ranked stats are now available via the ranked stats endpoint.
- leaderboard.included.player.attributes.stats.kda
- leaderboard.included.player.attributes.stats.tier
- leaderboard.included.player.attributes.stats.subTier

Data Changes:

- Leaderboards require :ref:`platform-region-shard` for seasons beginning with Season 7. API responses will include the top 500 players for each leaderboard. The page filter is no longer necessary.

Deprecated:

- playerSeason.attributes.gameModeStats.{gameMode}.rankPoints
- playerSeason.attributes.gameModeStats.{gameMode}.rankPointsTitle
- playerSeason.attributes.bestRankPoint



v19.1.0
--------

New Data:

- [Stadia] Data from Stadia matches and for Stadia players is now available.


v19.0.0
--------

New Data:

- [Console] If LogPlayerKill or LogPlayerMakeGroggy is triggered by a vehicle, and the engine was turned off, then the value "VehicleEngineOff" is added to damageCauserAdditionalInfo.

Data Changes:

- [Console] LogMatchEnd.characters and LogMatchStart.characters have been changed from an array of Character objects to an array of CharacterWrapper objects.



v18.1.0
--------

Deprecated:

- LogMatchDefinition.PingQuality



v18.0.0
--------

Data Changes:

- [PC] LogMatchEnd.characters and LogMatchStart.characters have been changed from an array of Character objects to an array of CharacterWrapper objects.



v17.2.0
--------

New Data:

- LogPlayerUseFlareGun
- Vehicle.velocity
- Vehicle.altitudeAbs
- Vehicle.altitudeRel
- Vehicle.isEngineOn
- [PC] If LogPlayerKill or LogPlayerMakeGroggy is triggered by a vehicle, and the engine was turned off, then the value "VehicleEngineOff" is added to damageCauserAdditionalInfo.



v17.1.0
--------

New Data:

- Match.attributes.matchType



v17.0.0
--------

Removed:

- Vehicle.rotationPitch



v16.2.0
--------

New Data:

- [PS4, Xbox] LogBlackZoneEnded
- [PS4, Xbox] LogPlayerDestroyBreachableWall
- [PS4, Xbox] LogPlayerKill.isThroughPenetrableWall
- [PS4, Xbox] LogPlayerMakeGroggy.isThroughPenetrableWall
- [PS4, Xbox] LogPlayerTakeDamage.isThroughPenetrableWall
- [PS4, Xbox] GameState.blackZonePosition
- [PS4, Xbox] GameState.blackZoneRadius



v16.1.0
--------

New Data:

- [PC] LogBlackZoneEnded
- [PC] LogPlayerDestroyBreachableWall
- [PC] LogPlayerKill.isThroughPenetrableWall
- [PC] LogPlayerMakeGroggy.isThroughPenetrableWall
- [PC] LogPlayerTakeDamage.isThroughPenetrableWall
- [PC] GameState.blackZonePosition
- [PC] GameState.blackZoneRadius



v16.0.0
-------

Bug Fix:

- Fixed the issue where the /leaderboards endpoint was not available for steam.

Data Changes:

- [PC] The season ID is now required for requests to the /leaderboards endpoint.

New Data:

- [PS4, Xbox, Kakao] Kakao and Console (PS4 and Xbox) leaderboards are now available using the /leaderboards endpoint.



v15.3.1
--------

Bug Fix:

- Fixed the issue where there were missing matches for some players, players were missing from LogMatchEnd, and there was no participant object for some players. This fix does not apply to previous matches.



v15.3.0
--------

New Data:

- [PS4, Xbox] LogPhaseChange
- [PS4, Xbox] LogPlayerUseThrowable



v15.2.0
--------

New Data:

- [PC] LogPhaseChange
- [PC] LogPlayerUseThrowable



v15.1.0
--------

New Data:

- [PS4, Xbox] LogObjectInteraction
- [PS4, Xbox] Vehicle.vehicleUniqueId
- [PS4, Xbox] Vehicle.rotationPitch
- [PS4, Xbox] Vehicle.isWheelsInAir
- [PS4, Xbox] Vehicle.isInWaterVolume



v15.0.0
--------

New Data:

- [PS4, Xbox] The Weapon Mastery endpoint is available.
- [PS4, Xbox] The "console" shard can be used, in addition to "xbox" and "psn", at the /matches endpoint for console matches.

Data Changes:

- [PS4, Xbox] The "console" shard must be used to get sample data for PS4/Xbox.
- [PS4, Xbox] Individual players' platforms can be determined from participant.shardId



v14.2.0
--------

New Data:

- LogItemPickupFromLootbox.creatorAccountId
- [PC] The Weapon Mastery endpoint is available.
- [PC] LogObjectInteraction
- [PC] Vehicle.vehicleUniqueId
- [PC] Vehicle.rotationPitch
- [PC] Vehicle.isWheelsInAir
- [PC] Vehicle.isInWaterVolume



v14.1.0
--------

New Data:

- LogVehicleLeave.fellowPassengers
- LogVehicleRide.fellowPassengers
- [PS4, Xbox] LogPlayerKill.VictimWeapon
- [PS4, Xbox] LogPlayerKill.VictimWeaponAdditionalInfo
- [PS4, Xbox] LogPlayerMakeGroggy.VictimWeapon
- [PS4, Xbox] LogPlayerMakeGroggy.VictimWeaponAdditionalInfo



v14.0.0
--------

Bug Fixes:

- Fixed the issue where the value of bestRankPoint is not always up to date across all game modes.

New Data:

- playerSeason.attributes.bestRankPoint
- [PC] LogPlayerKill.VictimWeapon
- [PC] LogPlayerKill.VictimWeaponAdditionalInfo
- [PC] LogPlayerMakeGroggy.VictimWeapon
- [PC] LogPlayerMakeGroggy.VictimWeaponAdditionalInfo

Data Changes:

- [PC] The remastered Erangel map will be called "Baltic_Main" and not "Erangel_Main".

Removed:

- playerSeason.attributes.gameModeStats.{gameMode}.bestRankPoint



v13.0.1
-------

Bug Fixes:

- Fixed the issue where "kill steals" would sometimes lead to inaccurate values for attributes.stats.kills in the participant object.



v13.0.0
--------

Data Changes:

- participant.attributes.stats.deathType will be "byzone" for players killed by the red or blue zones instead of "byplayer".



v12.0.0
-------

New Data:

- Lifetime stats for a single game mode can be requested in batches for up to 10 players using the new /seasons/lifetime/gameMode/{gameMode}/players endpoint.

Data Changes:

- LogPlayerKill.Assistant, LogPlayerKill.Killer, and LogPlayerPosition.Vehicle will be set to null instead of an empty object.

Removed:

- participant.attributes.stats.killPoints
- participant.attributes.stats.killPointsDelta
- participant.attributes.stats.lastKillPoints
- participant.attributes.stats.lastWinPoints
- participant.attributes.stats.mostDamage
- participant.attributes.stats.rankPoints
- participant.attributes.stats.winPoints
- participant.attributes.stats.winPointsDelta



v11.1.0
-------

New Data:

- Season stats for a single game mode can be requested in batches for up to 10 players using the new /seasons/{seasonId}/gameMode/{gameMode}/players endpoint.

- The number of players that information can be requested for using the /players endpoint has been increased from 6 to 10 players.



v11.0.1
-------

Bug Fixes:

- Fixed the issue where LogItemDrop events were missing for attachments that were dropped at the same time as detaching them from a weapon.



v11.0.0
--------

Bug Fixes:

- Fixed the issue where content decoding would fail for some telemetry files.

Data Changes:

- attributes.gameMode will have additional enums for custom matches in the match object. "normal" will be split into "normal", "war", "zombie", "conquest", and "esports". They will each prepend "-solo", "-duo", "-squad", and "-fpp" as the other enums do.



v10.0.1
-------

Bug Fixes:

- Fixed the issue where attributes.isCustomMatch was false and attributes.gameMode was "normal" in the match object for most matches at the /tournaments endpoint.



v10.0.0
-------

Data Changes:

- [PC] The /leaderboards endpoint will return up to 500 lone survivors per page requested.



v9.1.0
-------

Deprecated:

- Using the platform-region shard at the /samples endpoint is deprecated and the API will respond by returning data for all regions for the platform as if queried using the platform shard.



v9.0.0
------

New Data:

- [PS4, Xbox] Character.isInBlueZone
- [PS4, Xbox] Character.isInRedZone
- [PS4, Xbox] Character.zone
- [PS4, Xbox] GameResult
- [PS4, Xbox] LogHeal
- [PS4, Xbox] LogItemPickupFromCarepackage
- [PS4, Xbox] LogItemPickupFromLootbox
- [PS4, Xbox] LogMatchDefinition.SeasonState
- [PS4, Xbox] LogObjectDestroy
- [PS4, Xbox] LogParachuteLanding
- [PS4, Xbox] LogPlayerAttack.fireWeaponStackCount
- [PS4, Xbox] LogPlayerKill.assistant
- [PS4, Xbox] LogPlayerKill.damageCauserAdditionalInfo
- [PS4, Xbox] LogPlayerKill.dBNOId
- [PS4, Xbox] LogPlayerKill.victimGameResult
- [PS4, Xbox] LogPlayerMakeGroggy.damageCauserAdditionalInfo
- [PS4, Xbox] LogPlayerMakeGroggy.damageReason
- [PS4, Xbox] LogPlayerRevive.dBNOId
- [PS4, Xbox] LogRedZoneEnded
- [PS4, Xbox] LogSwimEnd.maxSwimDepthOfWater
- [PS4, Xbox] LogVaultStart
- [PS4, Xbox] LogVehicleLeave.maxSpeed
- [PS4, Xbox] LogWeaponFireCount
- [PS4, Xbox] Stats
- [PS4, Xbox] match.attributes.seasonState
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.bestRankPoint
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.dailyWins
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.rankPoints
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.swimDistance
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.weeklyWins
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.rankPointsTitle
- [PS4] Lifetime Stats as of division.bro.official.playstation-01 are available per gameMode by using "lifetime" as the seasonId at the /players/{accountId}/seasons/{seasonId} endpoint.
- [Xbox] Lifetime Stats as of division.bro.official.xbox-01 are available per gameMode by using "lifetime" as the seasonId at the /players/{accountId}/seasons/{seasonId} endpoint.

Data Changes:

- [PS4, Xbox] Season stats from Jan 22,2019 onwards will be global and sharded by platform. PS4 and Xbox data prior to Jan 22,2019 will still only be accessible using the old URL format.
- [PS4] PS4 seasons after division.bro.official.2018-09 will be in the format division.bro.official.playstation-{Season number} rather than division.bro.official.{Year-Month}. The first season after division.bro.official.2018-09 is division.bro.official.playstation-01.
- [Xbox] Xbox seasons after division.bro.official.2018-08 will be in the format division.bro.official.xbox-{Season number} rather than division.bro.official.{Year-Month}. The first season after division.bro.official.2018-089 is division.bro.official.xbox-01.

Deprecated:

- [PS4, Xbox] participant.attributes.stats.killPoints
- [PS4, Xbox] participant.attributes.stats.killPointsDelta
- [PS4, Xbox] participant.attributes.stats.winPoints
- [PS4, Xbox] participant.attributes.stats.winPointsDelta
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.killPoints
- [PS4, Xbox] playerSeason.attributes.gameModeStats.{gameMode}.winPoints



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
- [PC] LogItemPickupFromCarepackage
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

Data Changes:

- [PC] playerSeason.attributes.gameModeStats.{gameMode}.rankPoints will no longer be 0 when roundsPlayed < 10



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
