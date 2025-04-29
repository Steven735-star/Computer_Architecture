# Output Register Display Programming for EEPROM and 7-Segment Displays

This project provides an Arduino-based solution to program an EEPROM to store digit patterns for displaying decimal numbers on 7-segment displays.  
It supports both **unsigned** and **two's complement** 8-bit values.

## Overview

- **Shift registers** are used to manage address lines and output enable signals.
- **EEPROM programming** includes:
  - Unsigned decimal digits (0 to 255).
  - Signed 8-bit integers in two's complement (-128 to 127).
- **7-segment display encoding** is applied for each decimal digit.
- **Serial monitoring** allows for verification of EEPROM contents.

## Pinout

| Signal         | Arduino Pin |
|----------------|-------------|
| SHIFT_DATA     | 2           |
| SHIFT_CLK      | 3           |
| SHIFT_LATCH    | 4           |
| EEPROM_D0      | 5           |
| EEPROM_D7      | 12          |
| WRITE_EN       | 13          |

## Functions

- `setAddress(int address, bool outputEnable)`  
  Controls the shift registers to set the target EEPROM address.

- `readEEPROM(int address)`  
  Reads a byte from the specified EEPROM address.

- `writeEEPROM(int address, byte data)`  
  Writes a byte to the specified EEPROM address.

- `printContents()`  
  Reads and prints the entire EEPROM contents to the serial monitor.

## Programming Details

During the `setup()` phase, the EEPROM is programmed in the following sections:
1. **Unsigned numbers (0 to 255):**
   - Units place (0–9)
   - Tens place (00–90)
   - Hundreds place (000–200)
   - Sign indicator (always blank for unsigned)

2. **Two's complement numbers (-128 to 127):**
   - Units, tens, hundreds places
   - Sign indicator (`-` if negative)

Each decimal digit is encoded into a **common cathode 7-segment** format.

## Usage

1. Connect the Arduino to the EEPROM and shift register circuitry as described.
2. Upload the code to your Arduino.
3. Open the Serial Monitor (57600 baud).
4. The Arduino will:
   - Program the EEPROM.
   - Display the programmed data over the serial monitor for verification.

## Notes

- Common cathode encoding is used for the 7-segment displays.
- Timing critical operations (like `WRITE_EN` pulse) are managed with microsecond delays.
- The `loop()` function is empty as all operations are performed once during `setup()`.

## License

This project is open-source under the [MIT License](LICENSE).
