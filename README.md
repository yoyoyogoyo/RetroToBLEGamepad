\# Retro Console Controller → BLE Gamepad



Firmware that lets an ESP32 convert retro console controllers into a Bluetooth LE HID gamepad for your PC, phone, or other device.



Supports \*\*Sega Mega Drive / Genesis\*\* (3-button \& 6-button), \*\*Super Nintendo (SNES)\*\*, and passive DB9 controllers including \*\*Atari 2600\*\*, \*\*Sega Master System\*\*, and other Atari-spec DB9 joysticks (e.g. Commodore 64).



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

| 5       | +5V           | \*\*3V3\*\*    | \*\*Use 3.3V, NOT 5V!\*\* |

| 6       | Data0 (TL)    | 27         | MD: B / SMS \& Atari: Button 1 (Fire) |

| 7       | Select (TH)   | 13         | Output (TH multiplexer driver) |

| 8       | GND           | GND        |       |

| 9       | Data1 (TR)    | 14         | MD: C / SMS: Button 2 |



\### SNES Controller Port



| Signal | ESP32 GPIO | Direction |

|:-------|:----------:|:---------:|

| Latch  | 18         | Output    |

| Clock  | 19         | Output    |

| Data   | 21         | Input     |

| +5V    | \*\*3V3\*\*    | Power     |

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



