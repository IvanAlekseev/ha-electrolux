# Release Notes v3.7.4

## Features

- feat(rvc): gen 1 Pure i9 ecoMode support + ruff 0.16 upgrade (#158) by @netflash
  - Adds support for 1st-generation Pure i9 robots that report `ecoMode` (boolean) instead of `powerMode` (integer). Fan speed now maps to Eco/Power for gen 1, with an API workaround for setting power mode. Also bumps ruff to 0.16.0 and fixes Python 3.14 `except` syntax across 6 files.

- feat(rvc): human-readable Pure i9 power modes + new catalog entities (#156) by @netflash
  - Fan speed labels now show Eco/Standard/Power instead of raw integers, with bidirectional API↔UI mapping. New catalog entities for ecoMode, mute, and maintenance counters (mainBrushSqM, sideBrushSqM, filterSqM).

- feat(rvc): add Gordias/700series catalog entries (#152) by @netflash
  - Adds catalog support for Electrolux UltimateHome 700 Robotic Vac and Mop (Gordias): new binTank sensor, findMe button, setVoiceVolume select, plus expanded cleaningCommand, vacuumMode, and waterPumpRate values.

- feat(vacuum): zone-based cleaning service for PUREi9 (CustomPlay) (#148) by @netflash
  - New `electrolux.start_zone_cleaning` entity service for PUREi9 robots, sending CustomPlay commands with persistent map UUID and per-zone power modes.

- feat(translations): extend and update translations (#172) by @TTLucian
  - Adds new translation keys (control_disabled_by_mode, fanspeed_disabled, services.start_zone_cleaning) and extends/updates translations for 27 languages.

## Bug Fixes

- fix(api): stop reporting command failures as authentication errors (#161) by @tanarchytan
  - Command validation failures (e.g. "Remote control disabled") no longer surface as "Token expired or invalid" reauthentication prompts. The real error is now propagated correctly.

- fix(climate): replace deprecated CONCENTRATION constants with UnitOfDensity/UnitOfRatio (#171) by @TTLucian
  - Replaces deprecated `homeassistant.const` constants (CONCENTRATION_MICROGRAMS_PER_CUBIC_METER, CONCENTRATION_PARTS_PER_BILLION, CONCENTRATION_PARTS_PER_MILLION) with `UnitOfDensity`/`UnitOfRatio` equivalents in AC and air purifier catalogs.

- fix(number): keep delayed start adjustable when no programme declares it (#163) by @tanarchytan
  - `number.*_finish_in_delay` (stopTime capability) is no longer stuck at min=0/max=0 when the appliance advertises it as a global setting but no programme declares it.

- fix(sensor): suggest minutes for duration sensors reporting in seconds (#168) by @netflash
  - Duration sensors that report in seconds now suggest minutes as the display unit, making them easier to read in the UI while preserving the native unit.

- fix(td): add missing 65410 code to fcOptisenseLoadWeight catalog values (#155) by @netflash
  - Adds status code 65410 to the TD dryer catalog for `fcOptisenseLoadWeight`, ensuring the capability is properly matched.

- fix(vacuum): register zone cleaning with an entity service schema (#162) by @tanarchytan
  - Fixes a Home Assistant 2026.8.0 compatibility issue where the vacuum platform failed to load entirely due to the `start_zone_cleaning` service registering with a non-entity-service schema.

- fix: reduce SSE watchdog log spam and add exponential backoff (#153) by @netflash
  - SSE watchdog restart messages are now logged at INFO instead of WARNING, with exponential backoff (15min → 30min → 1h → 2h capped) and summary logging every 5 restarts.


## Contributors

@tanarchytan made their first contributions. A big THANK YOU!!

Thanks to all contributors who made this release possible:

- @TTLucian
- @netflash
- @tanarchytan
- @Copilot

