# Loki iPhone Control

Experimental iOS 27 screen-sharing modules and an ESP32-S3 HID bridge.

The source bundle contains:

- Native ScreenCaptureKit capture with explicit system sharing, bounded image processing, and fresh-frame checks.
- A CoreBluetooth command client with sequence-matched board replies and cancellation.
- A native connection and local latency-test panel.
- Two N16R8 firmware variants: phone-to-board BLE control, or computer UART-to-board USB HID control.
- Portable protocol tests and a PING-only USB transport probe.

Download and unpack `iphone-control-source.zip` to inspect and build the source.
Original HID implementation attribution and MIT license are included in `firmware/NOTICE.md` and `firmware/LICENSE.iscrcpy`.

## Status

This is a development candidate, not a finished autonomous phone agent. The firmware has been compiled locally and protocol invariants tested. Native iOS SDK validation, installation, pointer calibration, and actual device latency measurements remain required. The panel measures transport and supervised local clicks; it does not measure model decision latency. The native modules are not yet integrated into a signed application.

## Build

After unpacking the source:

```sh
python -m pip install platformio==6.2.0
cd firmware
python -m platformio run -e loki-s3-n16r8 -e loki-s3-wired
```

For the iOS modules, use Xcode 27 and iOS 27. The application integrating them needs Bluetooth usage text, screen-capture usage text, and the appropriate screen-capture / Bluetooth-central background modes.

The BLE variant requires pairing the accessory in iPhone AssistiveTouch and connecting the custom service in the app. It uses no Wi-Fi credentials. The wired variant uses the UART bridge for computer commands and the separate native USB port for phone HID. A compatible Lightning host adapter may be needed. HID does not carry screen video.

Before flashing, identify the board and preserve its existing firmware privately. These sources contain no credentials or personal device receipts. Do not commit pairing tokens, signing materials, screen captures, or firmware dumps.
