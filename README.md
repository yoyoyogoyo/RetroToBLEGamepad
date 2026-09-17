# Retro console controller → BLE gamepad

Firmware that converts retro console controllers into a Bluetooth LE HID gamepad for your PC, phone, or other device, using an ESP32.
---

## Supported Controllers \& Compatibility
- \*\*Sega Mega Drive / Genesis\*\*: 3-button and 6-button controllers.
- \*\*Super Nintendo (SNES)\*\*: Standard SNES controllers. 
- \*\*Sega Master System \& Atari 2600\*\*: Supported via the DB9 port
- \*\*Commodore 64 \& other Atari-standard DB9 joysticks\*\*: Structurally identical to Atari 2600/SMS pinouts, so they should work, though they have not been specifically tested.
- \*\*Nintendo Entertainment System (NES)\*\*: Should work using the SNES pins, but hasn't been tested.

## Hardware needed
- ESP32 Development board (I used a 30 pin)
- for Sega, Atari: a DB9 port or cut extension cable
- for SNES or NES: a SNES/NES controller port or cut extension cable.
- Cables/crimp connecters/solder to connect wires to board

---
## Setup instructions

- 1\. Install Arduino IDE and the ESP32 board package (by Espressif, I used v2.0.7).
- 2\. Install \*\*"ESP32 BLE Gamepad"\*\* by lemmingDev via the Arduino Library Manager. (I used v 0.5.4)
- 3\. Open `RetroToBLEGamepad.ino`, select your ESP32 board, and upload.
- 4\. Connect the controller port pins to the relevant ESP32 GPIO pins outlined below.
- 4\. Pair the ESP32 ("MegaDrive Pad") from your target device's Bluetooth settings.

---
## Wiring Guide
### Mega Drive / Genesis / Master System / Atari / C64
DB9 Controller Port (Front View / Female Socket)
```text
_______________________
 \\  1   2   3   4   5  /
 \\   6   7   8   9   /
  \ \_________________/
```
Pin 1: Up           -> GPIO 32
Pin 2: Down         -> GPIO 33
Pin 3: Left         -> GPIO 25
Pin 4: Right        -> GPIO 26
Pin 5: +5V          -> ESP32 3V3 (NOT 5V!)
Pin 6: Data0 / Fire -> GPIO 27
Pin 7: Select / TH  -> GPIO 13
Pin 8: GND          -> GND
Pin 9: Data1 / TR   -> GPIO 14

### SNES/NES
#### SNES Controller Port (Front View / Console Socket)
```text
+-----------------------------------+
 |  (1)  (2)  (3)  (4)  (5)  (6)  (7) |
+-----------------------------------+
[ Round Side ]            [ Flat Side ]
```
Pin 1: +5V   -> ESP32 3V3 (NOT 5V!)
Pin 2: Clock -> GPIO 19
Pin 3: Latch -> GPIO 18
Pin 4: Data  -> GPIO 21
Pin 5: N/C   -> (Unused)
Pin 6: N/C   -> (Unused)
Pin 7: GND   -> GND

#### NES Controller Port (Front View / Console Socket)
```text
+-----------------------+
 |  (1)  (2)  (3)  (4)   |
 |                       |  [ Flat Side ]
 |     (5)   (6)   (7)   |
 +-----------------------+
```
Pin 1: GND   -> GND
Pin 2: Clock -> GPIO 19
Pin 3: Latch -> GPIO 18
Pin 4: Data  -> GPIO 21
Pin 5: +5V   -> ESP32 3V3 (NOT 5V!)
Pin 6: N/C   -> (Unused)
Pin 7: N/C   -> (Unused)

---
## Button Mapping

Inputs from connected controllers are merged together, allowing controllers to be plugged in simultaneously. So you can have two of your original controllers connected (one MD/SMS/Atari or C64, and one SNES or NES), then just choose the one that you want for a given game. 

| Controller Button | BLE Gamepad Output |
|:------------------|:-------------------|
| \*\*D-Pad / Joystick\*\* (MD / SNES / Atari / SMS) | Hat Switch |
| \*\*MD A\*\* / \*\*SNES B\*\* / \*\*Atari Fire/SMS Button 1\*\* | Button 1 |
| \*\*MD B\*\* / \*\*SNES A\*\* / \*\*SMS Button 2\*\* | Button 2 |
| \*\*MD C\*\* / \*\*SNES L\*\* | Button 3 |
| \*\*MD Start\*\* / \*\*SNES Start\*\* | Button 4 |
| \*\*MD X\*\* / \*\*SNES Y\*\* | Button 5 |
| \*\*MD Y\*\* / \*\*SNES X\*\* | Button 6 |
| \*\*MD Z\*\* / \*\*SNES R\*\* | Button 7 |
| \* \*\*SNES Select\*\* | Button 8 |
---

