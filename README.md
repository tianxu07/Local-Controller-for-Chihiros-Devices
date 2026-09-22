# Local Controller for Chihiros Devices

**Control supported Chihiros aquarium lights and cooling fans from Windows without the My Chihiros app.**

Local Controller for Chihiros Devices is a free, open-source Windows application for controlling supported Chihiros devices directly over Bluetooth Low Energy (BLE).

No Chihiros account, login, internet connection, or cloud service is required.

**Unofficial community project. Not affiliated with Chihiros Aquatic Studio.**

Created by **Tianxu Yang**
Instagram: **@tianxu_07**

## Download

Windows 10 / 11 x64 with Bluetooth LE is required.

Python is not required for the packaged application.

The latest release is **v1.4.1**.

For v1.4.1, the recommended download is:

```text
ChihirosLocalController-1.4.1-windows-x64.zip
```

Extract the entire ZIP and run:

```text
ChihirosLocalController.exe
```

Keep the `_internal` folder next to the executable.

A standalone one-file version is also available:

```text
ChihirosLocalController-1.4.1-windows-x64-onefile.exe
```

The one-file version may take slightly longer to start.

Downloads can be verified using:

```text
SHA256SUMS.txt
```

The application is unsigned, so Windows may display a SmartScreen warning.

## Supported Chihiros Devices — Physically Tested

The following devices have been tested by me on real hardware:

* Chihiros RGB Vivid II
* Chihiros A2 Max
* Chihiros Magnetic Light
* Chihiros Magnetic Light II
* Chihiros Z Light
* Chihiros Cooling Fan

These device implementations were developed and physically validated using the actual hardware.

If you only use these devices and prefer a release containing only physically tested implementations, **v1.3.0 is the recommended stable version**.

## Additional Supported Chihiros Devices

Starting with v1.4.0, the project also includes support based on publicly available open-source protocol information for:

* A II
* A Series
* New C
* RGB + A PLUS
* SEA_LED (`DYSEA`, upstream device label)
* WRGB II
* C II
* Commander 4
* WRGB VIVID III
* RGB VIVID
* Commander X
* X300

Some device families use separate legacy and newer protocol profiles internally.

These additional device profiles have passed the project's automated protocol and safety tests, but **have not been physically tested by me on the corresponding hardware**.

Compatibility with every hardware or firmware revision cannot be guaranteed.

For WRGB II, the project currently supports the regular WRGB II profiles implemented by this project.

**WRGB II Pro, WRGB II Slim, and Universal WRGB are not supported.**

WRGB VIVID III support also includes integrated fan controls and passive RPM / temperature telemetry.

If you own one of these upstream-derived devices and successfully test it, feedback is welcome.

## Which Version Should I Download?

### v1.3.0 — Physically Tested Devices Only

Use **v1.3.0** if you only need the six devices that I have personally tested on real hardware:

* RGB Vivid II
* A2 Max
* Magnetic Light
* Magnetic Light II
* Z Light
* Chihiros Cooling Fan

v1.3.0 contains only the physically validated device implementations and does not include the additional upstream-derived device profiles introduced in v1.4.0.

For these six devices, **v1.3.0 is the recommended stable release** if you prefer the most conservative option.

### v1.4.1 — Additional Device Support

Use **v1.4.1** if you want support for the additional device profiles listed above.

v1.4.1 retains all physically tested device support from v1.3.0 and adds the additional upstream-derived device implementations introduced in v1.4.0.

These additional profiles have not yet been physically tested by me on their corresponding hardware.

## Basic Usage

1. Close the **My Chihiros** app on nearby phones or tablets.
2. Enable Bluetooth on the Windows PC.
3. Power on the Chihiros device.
4. Launch **Local Controller for Chihiros Devices**.
5. Click **Scan for Devices**.
6. Select the device.
7. Adjust the available controls.
8. Click the appropriate **Apply** button.

Scanning, selecting a device, or moving sliders does not send control commands until an Apply action is used.

Multiple devices are kept separate using their full BLE addresses.

## Schedule Support

Light schedule editing is **not supported**.

Local Controller for Chihiros Devices is mainly intended for direct, manual local control of supported Chihiros devices without requiring the My Chihiros app to remain connected.

For simple daily power on/off timing, using a **smart plug** is recommended.

If you want to create, edit, or restore the light's normal schedule, use the official **My Chihiros** application after the local Bluetooth connection has ended.

## Important Notes

Manual control may override the device's existing automatic schedule.

Manual settings may remain stored on the device after disconnecting or power cycling.

To return to normal schedule-driven operation, use **My Chihiros**.

The application does not provide:

* Light schedule editing
* Firmware / DFU functions
* Pairing reset
* Device rename
* Raw packet control
* Automatic write retry

A failed BLE write may still have reached the device, so check the physical result before retrying.

## Current Version

**v1.4.1**

Version 1.4.1 includes all physically tested device support from v1.3.0 together with the additional device profiles introduced in v1.4.0.

The additional v1.4.x device profiles are based on publicly available open-source protocol information and have passed the project's automated protocol and safety tests, but have not been physically tested by me on all corresponding hardware.

If you only want support for devices that I have personally tested on real hardware, **v1.3.0 remains the recommended stable release**.

## Why Use Local Controller for Chihiros Devices?

This project may be useful if you want to:

* Control supported Chihiros lights from a Windows PC
* Control Chihiros devices without keeping the My Chihiros app connected
* Use direct Bluetooth Low Energy communication
* Control devices without a Chihiros account
* Control devices without internet access or cloud services
* Perform simple manual brightness, color, or device control from Windows

The application communicates directly with supported devices over Bluetooth LE.

## From Source

From the repository root:

```powershell
python -m pip install -r requirements-build.txt
python -m unittest discover -s tests
python .\chihiros_local_controller.py
```

## Credits

Version 1.4.0 introduced independently implemented device support informed by publicly available open-source protocol information from:

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
