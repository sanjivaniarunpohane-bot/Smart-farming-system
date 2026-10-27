# N.A.P SMART FARMING RC — Android starter project

## What this is
Android Studio Java project source for a futuristic HC-05 Bluetooth Classic controller. It is source code, not a prebuilt APK. Build with Android Studio / compatible cloud Android build service.

## Before testing
1. Pair the HC-05 in Android Settings first (usual PIN is printed on module documentation; often 1234 or 0000).
2. Build and install this app, grant Nearby devices/Bluetooth permissions.
3. Raise the robot securely so wheels cannot propel it, keep spray/seed mechanisms disconnected for the first test.
4. Connect to the paired HC-05. A connection confirms only the Bluetooth link, not Arduino or motor functionality.
5. Verify motor direction and STOP with the actual firmware.

## Command protocol currently in this starter
Drive press: F forward, B backward, L left, R right, Q forward-left, E forward-right, Z back-left, C back-right. On release, sends S.
Spray: P on, p off. Seed: N on, n off.
Horn: V on, v off.
Front/rear light UI buttons are currently placeholders because each needs separate ON and OFF actions. Add those after confirming the Arduino mapping.

## Required firmware alignment
The app's revised diagonal and seed commands intentionally avoid conflicts in the original list. Your Mega firmware must implement the same characters. The original list had G shared by forward-left and seed ON, and W shared by forward and headlights in the alternate mapping. Do not drive until app and firmware mappings match.

## Safety / limitations
- This starter does not receive/parse Arduino acknowledgements yet; TEST LINK sends '?' only. For a true diagnostic result, add firmware that replies with e.g. `NAP:OK\n` and implement reading/parsing in the app.
- On disconnect the app attempts to send S, but cannot guarantee delivery if the radio link is already lost. Implement an Arduino-side watchdog timeout that stops drive, spray and seed outputs if commands stop arriving.
- The pin map for the L293D shield must be confirmed against the exact shield. PWM pins 2 and 3 and the stated direction pins are not universal across 4WD shields.
- Test with wheels raised, then at low speed in a clear area. Keep people and animals clear.
