# Release Notes v3.7.7

## 🛠 Fixes

- __fix(api): only treat exact ON/OFF write capabilities as switches (#201)__ by @TTLucian Write-only capabilities with exactly `{ON, OFF}` values are now modeled as a single optimistic SWITCH instead of two separate BUTTON entities. Multi-command sets that include ON/OFF among other commands (e.g. `{ON, OFF, PAUSE, RESUME, START, STOPRESET}`) remain command buttons — sending "ON" there yielded `406 COMMAND_VALIDATION_ERROR` in states where the appliance only accepts START/STOPRESET (see issue #200).
- __fix(entity): extract real PNC/serial from applianceData for Telica (#199)__ by @TTLucian For long numeric applianceIds (Telica, Muju, etc.), device info now shows the human-readable PNC from `applianceData.pnc` (e.g. `Telica-950011709`) instead of the full applianceId, and the serial number from `applianceData.sn`.

## ✨ Features

- __feat(telica): add Telica portable AC support (#199)__ by @TTLucian New appliance type __Telica__ (Electrolux 700 Silent Portable AC) is now fully supported: climate control, air quality sensors (PM2.5/PM10), filter maintenance tracking (main + HEPA), sound volume, sleep mode, vertical swing, flap position, scheduler, and timer controls. Threshold constants exposed as diagnostic sensors disabled by default.
- __feat(cr): add applianceUiSwVersion + blacklist fPRPN_/fSPN_ (#194)__ by @TTLucian Added `applianceUiSwVersion` diagnostic sensor to the CR (refrigerator) catalog. Internal push-notification flags (`fPRPN_AirFilterChange`, `fPRPN_WaterFilterOrder`, `fSPN_CRConnectionLost`, etc.) are now blacklisted so they don't appear as cryptic generic sensors.
- __feat(ov): proper catalog entry + default-disable for targetMicrowavePower (#193)__ by @TTLucian Microwave target power is now a properly cataloged NUMBER entity with min/max/step constraints from the API, disabled by default.

## 🔧 Internal / chores

- Removed built-in alert notifications due to API inconsistency. Alert state is still available via the alerts entity attribute — users can create custom automations with Home Assistant's notification system for more control and reliability.

## ⬆️ Upgrade notes

- __Telica portable AC owners__: after upgrading, device info will show the real PNC and serial number instead of one long code. Filter threshold entities appear disabled by default — enable them in HA if you want to see the reference values behind filter state changes.

## ⚠️ Special note
Many features and appliance types supported by this integration have __not been tested__ on physical appliances in the wild. Since I do not own most of the supported appliance types and models, development and testing often rely on diagnostic data, API capabilities, and reported appliance behaviour rather than direct testing on physical appliances.

I'm therefore __counting on the community__ to help validate these features. If you encounter anything unexpected, incorrect, missing, or broken, please report it with __as much detail as possible__, ideally including __diagnostics__ and relevant __debug logs__.

Even seemingly small issues or unusual appliance behaviour can be valuable, as they help improve compatibility and prevent incorrect assumptions and guesswork from becoming permanent parts of the integration.

If you own an appliance type that hasn't been tested, your feedback is especially valuable. See [README.md](https://github.com/TTLucian/ha-electrolux/blob/main/README.md) for more information.

## 🌟 Credits
BIG thank-yous to all contributors and to all supporters!

Without you, this project would not have been possible.