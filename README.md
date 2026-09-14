# Chihiros Local Controller 1.4.0

Chihiros Local Controller is a local Windows application for controlling supported
Chihiros aquarium lights and Cooling Fans directly over Bluetooth Low Energy.

No Chihiros account, login, internet connection, or Chihiros cloud service is required.

**Unofficial community tool. Not affiliated with Chihiros Aquatic Studio.**

Created by **Tianxu Yang** · Instagram: **[@tianxu_07](https://www.instagram.com/tianxu_07/)**

Version 1.4.0 keeps the six physically tested local implementations from v1.3.0
and adds additional device support based on publicly available open-source
protocol information.

The new upstream-derived device profiles have passed the project's automated
protocol and safety tests, but have **not been physically tested by me on the
corresponding hardware**.

If you only need the devices I have personally tested on real hardware,
**v1.3.0 remains the recommended stable release for that hardware set.**

---

## Physically tested devices

The following implementations have been tested by me on real hardware.

### Chihiros RGB Vivid II

- Manual Red / Green / Blue sliders
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

- Red / Green controls
- Range: 0–100
- Apply RG
- Verified prefix: `DYCX`
- Verified channel order:
  - Red = channel 0
  - Green = channel 1

The implementation was physically tested on a real device.

Local R20 / G40 visibly matched the official app's R20 / G40 setting during
testing.

Values above 100, including overclock-style values, are intentionally unsupported.

### Chihiros Magnetic Light II

- Red / Green / Blue / White controls
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

An official-app R20 / G40 / B60 / W30 comparison matched visible color and
apparent brightness in practical testing.

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

Supported device families include:

- A II
- A Series
- New C
- RGB + A PLUS
- SEA LED
- WRGB II
- C II
- Commander 4
- WRGB VIVID III
- RGB VIVID
- Commander X
- X300

Some device families have separate newer and legacy protocol profiles internally.

WRGB VIVID III support also includes:

- Manual light control
- Integrated fan control
- Fan Auto mode
- Temperature thresholds
- Passive fan RPM telemetry
- Passive temperature telemetry

Compatibility with every hardware or firmware revision cannot be guaranteed.

If you own one of these devices and test it successfully, feedback is welcome.

### Schedule support

Light schedule editing is **not supported** in v1.4.0.

The application is intended primarily for direct/manual local BLE control.

Manual light operation may override an existing device schedule. To return to
normal schedule-driven operation, use the official My Chihiros application after
the local connection has ended.

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
- Rename function
- Raw packet entry
- Automatic write retry
- Guessed transport fallback

A failed write may still have reached the physical device. Always check the
physical result before retrying.

---

## Windows package

Windows 10 / 11 x64 with Bluetooth LE is required.

Python is **not required** for the packaged application.

The recommended download is:

```text
ChihirosLocalController-1.4.0-windows-x64.zip
