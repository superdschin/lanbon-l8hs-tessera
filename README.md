# Lanbon L8-HS for Tessera / ESP Screens

Community configuration draft for the **Lanbon L8-HS three-relay variant**. The board profile has been tested on one physical device with the display, capacitive touch, all three relays, RGB outputs, ESPHome and Tessera Screen Manager working.

> **Status:** community-tested on one hardware revision; not yet registered as an officially selectable board in Tessera's `New screen` catalog. Other L8-HS revisions may differ. Verify your board before flashing.

## Hardware tested

- Board: Lanbon L8-HS, three-relay variant
- MCU: classic ESP32 (ESP32-D0WD), 8 MB flash
- Display: ST7789V, 240 × 320 pixels
- Touch controller: FT6336 capacitive touch
- Backlight: GPIO5
- Display SPI: CLK GPIO19, MOSI GPIO23, CS GPIO22, DC GPIO21, RESET GPIO18
- Touch I²C: SDA GPIO4, SCL GPIO0
- Relays: GPIO12, GPIO14, GPIO27
- RGB outputs: red GPIO26, green GPIO32, blue GPIO33

## Tested settings

- `ROTATION_LANDSCAPE: "270"`
- `TOUCH_SWAP_XY: "false"`
- `TOUCH_MIRROR_X: "true"`
- `TOUCH_MIRROR_Y: "true"`
- RGB output IDs match the shared Tessera feature: `output_red`, `output_green`, `output_blue`.

Tested on the author's device: display, touch alignment, all three relays, RGB colour mapping, ESPHome connection and Tessera integration.

## Files

- `packages/boards/lanbon-l8hs.yaml` — board-specific hardware and display settings. It uses shared files from the Tessera / ESP Screens source tree and is **not a standalone ESPHome package**.
- `profiles/display-sauna.example.yaml` — example per-device configuration. It uses the individual name `display-sauna`; copy it to your ESPHome configuration directory and adjust include paths to match your installation.

## Use with an existing Tessera / ESP Screens checkout

1. Back up your working configuration.
2. Copy `packages/boards/lanbon-l8hs.yaml` into the existing source tree at `homeassistant_espscreen/packages/boards/lanbon-l8hs.yaml` (or the corresponding path in your checkout).
3. Create an individual ESPHome file from `profiles/display-sauna.example.yaml`. Its board include points to the board file copied into the existing `homeassistant_espscreen` tree; keep that layout or adjust the path accordingly.
4. Put credentials in the local `secrets.yaml`. The example expects `api_encryption`, `wifi_ssid`, `wifi_password` and `fallback_ap_password`.
5. Validate and compile before flashing. Do not commit your real `secrets.yaml` or any local credentials.

## Selecting it directly in Tessera

This companion repository alone does not add the board to the Tessera Screen Manager's **New screen** catalog. That requires a reviewed contribution to the main Tessera / ESP Screens repository, including a `boards.yaml` entry and generated board entries/metadata. Until that integration is accepted, use the manual configuration above.

## Safety notes

- GPIO0 is a strapping pin; this profile marks the I²C SCL pin with `ignore_strapping_warning: true`. Verify startup behaviour on your hardware revision.
- Relay outputs can switch mains-powered loads. Confirm the hardware and electrical safety before connecting loads.
- The profile sets relay restore mode to `ALWAYS_OFF`.
- Never publish Wi-Fi credentials, API encryption keys, OTA passwords, or fallback AP passwords.

## License and upstream

This repository is a community companion for Tessera / ESP Screens. Before redistributing this profile or submitting it upstream, check the current license terms of the original Tessera / ESP Screens project. A repository-specific license has not yet been added.
