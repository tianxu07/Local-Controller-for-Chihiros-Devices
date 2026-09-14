# Chihiros Local Controller

A Windows application for controlling supported Chihiros aquarium lights and cooling fans directly over Bluetooth Low Energy.

No Chihiros account, login, internet connection, or cloud service is required.

**Unofficial community project. Not affiliated with Chihiros Aquatic Studio.**

Created by **Tianxu Yang**  
Instagram: **@tianxu_07**

## Current Version

**v1.4.0**

Version 1.4.0 keeps all of the physically tested device support from v1.3.0 and adds support for additional devices based on publicly available open-source protocol information.

If you only need the devices I have personally tested on real hardware, **v1.3.0 remains the recommended stable release for those devices.**

## Physically Tested Devices

The following devices have been tested by me on real hardware:

- Chihiros RGB Vivid II
- Chihiros A2 Max
- Chihiros Magnetic Light
- Chihiros Magnetic Light II
- Chihiros Z Light
- Chihiros Cooling Fan

These implementations were developed and physically validated using the actual devices.

## Additional Device Support in v1.4.0

Version 1.4.0 also adds support based on publicly available open-source protocol information for:

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

Some device families use separate legacy and newer protocol profiles internally.

These additional devices have passed the project's automated protocol and safety tests, but **have not been physically tested by me on the corresponding hardware**.

Compatibility with every hardware or firmware revision cannot be guaranteed.

For WRGB II, v1.4.0 supports the regular WRGB II profiles implemented by this project. **WRGB II Pro, WRGB II Slim, and Universal WRGB are not supported.**

WRGB VIVID III support also includes integrated fan controls and passive RPM / temperature telemetry.

If you own one of the upstream-derived devices and test it successfully, feedback is welcome.

## Schedule Support

Light schedule editing is **not supported**.

Chihiros Local Controller is mainly intended for direct/manual local control.

For simple daily on/off timing, using a **smart plug** is recommended.

If you want to create, edit, or restore the light's normal schedule, use the official **My Chihiros** application after the local Bluetooth connection has ended.

## Download

Windows 10 / 11 x64 with Bluetooth LE is required.

Python is not required for the packaged application.

The recommended download is:

```text
ChihirosLocalController-1.4.0-windows-x64.zip
```

Extract the entire ZIP and run:

```text
ChihirosLocalController.exe
```

Keep the `_internal` folder next to the executable.

A standalone version is also available:

```text
ChihirosLocalController-1.4.0-windows-x64-onefile.exe
```

The one-file version may take slightly longer to start.

Downloads can be verified using:

```text
SHA256SUMS.txt
```

The application is unsigned, so Windows may display a SmartScreen warning.

## Basic Usage

1. Close My Chihiros on nearby phones or tablets.
2. Enable Bluetooth on the Windows PC.
3. Power on the Chihiros device.
4. Launch Chihiros Local Controller.
5. Click **Scan for Devices**.
6. Select the device.
7. Adjust the available controls.
8. Click the appropriate **Apply** button.

Scanning, selecting a device, or moving sliders does not send control commands until an Apply action is used.

Multiple devices are kept separate using their full BLE addresses.

## Important Notes

Manual control may override the device's existing automatic schedule.

Manual settings may remain stored on the device after disconnecting or power cycling.

To return to normal schedule-driven operation, use **My Chihiros**.

The application does not provide:

- Light schedule editing
- Firmware / DFU functions
- Pairing reset
- Device rename
- Raw packet control
- Automatic write retry

A failed BLE write may still have reached the device, so check the physical result before retrying.

## From Source

From the repository root:

```powershell
python -m pip install -r requirements-build.txt
python -m unittest discover -s tests
python .\chihiros_local_controller.py
```

## Credits

Version 1.4.0 includes independently implemented device support informed by publicly available open-source protocol information from:

**TheMicDiet/chihiros-led-control**

https://github.com/TheMicDiet/chihiros-led-control

Cooling Fan protocol behavior was independently implemented in Python using publicly available research from:

**BartdeJonge/chihiros-esphome**

https://github.com/BartdeJonge/chihiros-esphome

Third-party licenses and required attribution are included in:

```text
THIRD_PARTY_LICENSES.txt
```

## License

Original project code is released under the MIT License.

Copyright © 2026 Tianxu Yang.

Third-party components retain their respective licenses.

Product names belong to their respective owners.

This software is provided **as is**, without warranty.
