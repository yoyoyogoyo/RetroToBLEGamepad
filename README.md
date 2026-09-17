# Mega Drive / Genesis Controller → BLE Gamepad

Firmware that lets an ESP32 read a stock Sega Mega Drive/Genesis controller
(3-button or 6-button) and present it to your PC/phone/console as a
Bluetooth LE gamepad. Also works with Sega Master system and Atari 2600 
joystick controllers

## Parts

- Any ESP32 dev board (classic ESP32; not S2, which has no Bluetooth)
- A Sega Mega Drive/Genesis controller (or a DB9 extension cable you can
  cut and wire up)
- A DB9 (9-pin) female connector/breakout if you want it detachable,
  or just solder directly to a cut cable

## Wiring

| DB9 Pin | Signal        | ESP32 GPIO |
|--------:|---------------|:----------:|
| 1       | Up            | 32         |
| 2       | Down          | 33         |
| 3       | Left          | 25          |
| 4       | Right         | 26         |
| 5       | +5V           | **3V3**    |
| 6       | Data0 (TL)    | 27         |
| 7       | Select (TH)   | 13         |
| 8       | GND           | GND        |
| 9       | Data1 (TR)    | 14         |

**Important:** power the controller from the ESP32's 3.3V pin, not 5V.
ESP32 GPIOs are not 5V tolerant, and Mega Drive pads work fine at 3.3V
(they're simple CMOS logic / switches internally).

DB9 pin numbering, viewed from the *front* of the female port on the
controller's plug (i.e. the pins you'd solder to on a breakout are
mirrored) — top row left-to-right is 1,2,3,4,5, bottom row is 6,7,8,9.
Double check with a multimeter/continuity tester against your specific
connector before powering it up.

Pins are configured as inputs with internal pull-ups; the controller
pulls a line low when a button or direction is pressed.

## Software setup

1. Install the Arduino IDE and the ESP32 board package.
2. In Library Manager, install **"ESP32 BLE Gamepad"** by lemmingDev.
   It will pull in NimBLE-Arduino as a dependency automatically.
3. Open `MegaDriveBLEGamepad.ino`, select your ESP32 board, and flash it.
4. Power the ESP32, then pair "MegaDrive Pad" from your device's
   Bluetooth settings like any other BLE gamepad.



   \# Retro Console Controller → BLE Gamepad



Firmware that lets an ESP32 convert retro console controllers into a Bluetooth LE HID gamepad for your PC, phone, or other device.



\---



\## Supported Controllers \& Compatibility



\- \*\*Sega Mega Drive / Genesis\*\*: 3-button and 6-button controllers.

\- \*\*Super Nintendo (SNES)\*\*: Standard SNES controllers.

\- \*\*Sega Master System \& Atari 2600\*\*: Supported via the DB9 port

\- \*\*Commodore 64 \& other Atari-standard DB9 joysticks\*\*: Structurally identical to Atari 2600/SMS pinouts, so they should work, though they have not been specifically tested.



\---



\## Wiring Guide



\### DB9 Port (Mega Drive / Genesis / Master System / Atari / C64)



| DB9 Pin | Signal        | ESP32 GPIO | Notes |
|--------:|---------------|:----------:|:------|
| 1       | Up            | 32         |       |
| 2       | Down          | 33         |       |
| 3       | Left          | 25         |       |
| 4       | Right         | 26         |       |
| 5       | +5V           | **3V3**    | **Use 3.3V, NOT 5V!** |
| 6       | Data0 (TL)    | 27         | MD: B / SMS & Atari: Button 1 (Fire) |
| 7       | Select (TH)   | 13         | Output (TH multiplexer driver) |
| 8       | GND           | GND        |       |
| 9       | Data1 (TR)    | 14         | MD: C / SMS: Button 2 |



\### SNES Controller Port


| Signal | ESP32 GPIO | Direction |
|:-------|:----------:|:---------:|
| Latch  | 18         | Output    |
| Clock  | 19         | Output    |
| Data   | 21         | Input     |
| +5V    | **3V3**    | Power     |
| GND    | GND        | Ground    |



> \\\\\\\*\\\\\\\*⚠️ Important:\\\\\\\*\\\\\\\* Power controllers from the ESP32's \\\\\\\*\\\\\\\*3.3V\\\\\\\*\\\\\\\* pin, not 5V. ESP32 GPIOs are not 5V tolerant, and retro pads run reliably at 3.3V logic levels.



\---



\## Button Mapping



Inputs from connected controllers are merged together using an logical OR operation, allowing controllers to be plugged in simultaneously:



| Controller Button | BLE Gamepad Output |

|:------------------|:-------------------|

| \*\*D-Pad / Joystick\*\* (MD / SNES / Atari / SMS) | Hat Switch |

| \*\*MD A\*\* / \*\*SNES B\*\* / \*\*Atari/SMS Fire\*\* | Button 1 |

| \*\*MD B\*\* / \*\*SNES A\*\* / \*\*SMS Button 2\*\* | Button 2 |

| \*\*MD C\*\* / \*\*SNES L\*\* | Button 3 |

| \*\*MD Start\*\* / \*\*SNES Start\*\* | Button 4 |

| \*\*MD X\*\* / \*\*SNES Y\*\* | Button 5 |

| \*\*MD Y\*\* / \*\*SNES X\*\* | Button 6 |

| \*\*MD Z\*\* / \*\*SNES R\*\* | Button 7 |

| \* \*\*SNES Select\*\* | Button 8 |



\---



\## Software Setup



1\. Install Arduino IDE and the ESP32 board package (by Espressif, I used v2.0.7).

2\. Install \*\*"ESP32 BLE Gamepad"\*\* by lemmingDev via the Arduino Library Manager. (I used v 0.5.4)

3\. Open `RetroToBLEGamepad.ino`, select your ESP32 board, and upload.

4\. Pair the ESP32 ("MegaDrive Pad") from your target device's Bluetooth settings.



