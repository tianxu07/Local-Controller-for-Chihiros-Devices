# Chihiros Local Controller 1.4.0

Chihiros Local Controller is a local Windows application for controlling supported
Chihiros aquarium lights and Cooling Fans directly over Bluetooth Low Energy.

No Chihiros account, login, internet connection, or Chihiros cloud service is required.

**Unofficial community tool. Not affiliated with Chihiros Aquatic Studio.**

Created by **Tianxu Yang** · Instagram: **@tianxu_07**

Version 1.4.0 keeps the six physically tested local implementations from v1.3.0
and adds additional device support based on publicly available open-source protocol
information.

The new upstream-derived device profiles have passed the project's automated
protocol and safety tests, but have **not been physically tested by me on the
corresponding hardware**.

If you only need the devices I have personally tested on real hardware,
**v1.3.0 remains the recommended stable release for that hardware set.**

---

## Physically tested devices

The following implementations have been tested by me on real hardware.

### Chihiros RGB Vivid II

- Manual Red / Green / Blue control
- Range: 0–100
- Verified advertisement prefixes:
  - `DYNV`
  - `DYNVVD`
  - `DYRGBV`

### Chihiros A2 Max

- Manual Brightness control
- Range: 1–100
- Verified prefix: `DYNCMC`

The implementation has been physically validated on one A2 Max unit.

Compatibility with every hardware or firmware revision is not guaranteed.

Brightness is represented as a normalized wire level internally and should not
be interpreted as a guarantee of exact official-app percentage equivalence.

### Chihiros Magnetic Light

Original / first-generation Magnetic Light.

- Red / Green control
- Range: 0–100
- Apply RG
- Verified prefix: `DYCX`
- Verified channel order:
  - Red = channel 0
  - Green = channel 1

The implementation was physically tested on a real device.

Local R20 / G40 visibly matched the official app's R20 / G40 setting during testing.

Values above 100, including overclock-style values, are intentionally unsupported.

### Chihiros Magnetic Light II

- Red / Green / Blue / White control
- Range: 0–100
- Apply WRGB
- Verified prefix: `DYMNC`
- Verified channel order:
  - Red = channel 0
  - Green = channel 1
  - Blue = channel 2
  - White = channel 3

Manual WRGB control has been physically validated on three Magnetic Light II units.

Testing confirmed that all three units could be independently selected and that
only the selected device changed.

An official-app R20 / G40 / B60 / W30 comparison matched visible color and apparent
brightness in practical testing.

This supports the practical direct 0–100 convention, not photometric linearity
or laboratory-calibrated equivalence.

### Chihiros Z Light

- Cool White
- Warm White
- Range: 0–100
- Apply White
- Verified prefix: `DYSSD`

The prefix classification and isolated white-channel control were physically
validated on a real Z Light.

### Chihiros Cooling Fan

Verified prefix: `DYNFAN`

Supported controls include:

- Manual fan speed: 0–20
- Device-side automatic thermostat configuration
- Start Temperature
- Max-Speed Temperature
- Refresh Status
- Room temperature telemetry
- Water temperature telemetry
- Humidity telemetry

The fan regulates itself after automatic configuration, so the PC does not need
to remain connected or powered on.

Threshold read-back is not currently supported. Start / Max values shown in the
GUI are locally remembered session values rather than values read back from the fan.

Silent Mode is not currently supported.

Cooling Fan support has been physically validated on a real device.

---

## Additional upstream-derived support in v1.4.0

Version 1.4.0 adds additional device support based on publicly available
open-source protocol information.

These implementations have passed automated protocol and safety tests but
**have not been physically tested by me on the corresponding hardware**.

Supported upstream-derived device families include:

- A II
- A Series
- New C
- RGB + A PLUS
- SEA_LED (`DYSEA`, upstream device label)
- WRGB II
- C II
- Commander 4
- WRGB VIVID III
- RGB VIVID
- Commander X
- X300

Some device families have separate legacy and newer protocol profiles internally.

### WRGB II scope

The upstream-derived WRGB II support in v1.4.0 applies to the regular WRGB II
profiles implemented by this project.

The following variants are **not supported** by the v1.4.0 upstream-derived path:

- WRGB II Pro
- WRGB II Slim
- Universal WRGB

### WRGB VIVID III

WRGB VIVID III support includes:

- Manual light control
- Integrated fan control
- Fan Auto mode
- Temperature thresholds
- Passive fan RPM telemetry
- Passive temperature telemetry

### Upstream devices intentionally not enabled in v1.4.0

Some devices are present in the upstream project but are intentionally not exposed
as writable devices in Chihiros Local Controller 1.4.0.

These include:

- Commander 1
- WRGB II Pro
- WRGB II Slim
- Universal WRGB
- C II RGB
- Z Light TINY
- Tiny Terrarium Egg

Upstream registry presence does not automatically mean that the device is supported
by this project.

The v1.4.0 implementation uses a fail-closed approach and only enables device
profiles for which the expected transport and protocol behavior were considered
sufficiently defined.

Compatibility with every hardware or firmware revision cannot be guaranteed.

If you own one of the upstream-derived supported devices and test it successfully,
feedback is welcome.

---

## Schedule support

Light schedule editing is **not supported** in v1.4.0.

The application is intended primarily for direct/manual local BLE control.

Manual light operation may override an existing device schedule.

For simple daily on/off timing, using a **smart plug** is recommended.

If you need to create, edit, or restore the light's normal schedule, use the
official **My Chihiros** application after the local connection has ended.

Chihiros Local Controller does not currently provide a light schedule editor or
write stored light schedules to supported devices.

---

## Device identification and safety

An unrelated Nordic UART device is never accepted simply because it exposes NUS.

Multiple devices, including multiple units of the same model or devices with
identical advertised names, remain distinct by their full BLE addresses.

Dropdown labels show the model and a short address suffix for convenience.
Displayed labels are presentation only and are never used as device identity keys.

RX / TX endpoints must be direct children of the expected BLE service.

The complete FE59 / DFU subtree is permanently blacklisted.

GATT handles are used for diagnostics only and are not treated as identity checks.

There is no:

- Firmware / DFU access
- Pairing reset
- Device rename
- Raw packet entry
- Automatic write retry
- Guessed transport fallback

A failed write may still have reached the physical device.

Always check the physical result before retrying a failed operation.

---

## Windows package

Windows 10 / 11 x64 with Bluetooth LE is required.

Python is **not required** for the packaged application.

The recommended download is:

```text
ChihirosLocalController-1.4.0-windows-x64.zip
