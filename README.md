# CompactDuino

Ultra-compact Arduino-compatible board built around the ATmega168PA-MU that fits on your breadboard. USB-C, onboard USB-UART, 3.3 V LDO and a WS2812B RGB LED on a ~23 mm × ~35 mm PCB.

## Features

- ATmega168PA-MU with 16 MHz external crystal
- USB-C (16-pin) connector, programming and power over USB
- CH340E USB-UART bridge with green Tx LED
- AP2112K LDO for 5 V → 3.3 V conversion (3.3 V rail marked as `3V`)
- WS2812B addressable RGB LED
- MCU reset button
- Optional USBLC6-2SC6 ESD protection on the USB data lines
- Breakout of Rx, Tx, D2–D13, A0–A7, GND, GND, 5V, 3V

### Optional ESD protection

The USBLC6-2SC6 footprint can be populated for ESD protection. If it is not used, bridge the pads as follows so the data lines stay connected:

- pin 1 ↔ pin 6
- pin 3 ↔ pin 4

## Bootloader installation

The ATmega168PA ships blank, so the bootloader has to be burned once using a second Arduino as an ISP programmer. After that the board can be programmed directly over USB.

### 1. Install board support

In the Arduino IDE open **File → Preferences → Additional Boards Manager URLs** and add:

```
https://mcudude.github.io/MiniCore/package_MCUdude_MiniCore_index.json
```

Then open the **Boards Manager**, search for **MiniCore** and install it.

### 2. Prepare the programmer Arduino

1. Open the Arduino IDE.
2. Plug in the programmer Arduino and select its COM port.
3. Upload **File → Examples → 11.ArduinoISP → ArduinoISP** to it.
4. Unplug the programmer.

### 3. Wiring

Connect the programmer to the CompactDuino:

| Programmer Arduino | CompactDuino |
|--------------------|--------------|
| D10 | Reset |
| D11 | D11 |
| D12 | D12 |
| D13 | D13 |
| 5V | 5V |
| GND | GND |

### 4. Burn the bootloader

1. Plug in the programmer. Both boards are now powered from the same 5 V rail.
2. Select the programmer's COM port.
3. **Tools → Board → MiniCore → ATmega168**
4. **Tools → Programmer → Arduino as ISP**
5. Click **Tools → Burn Bootloader**.
6. A success message confirms completion.

The board can now be programmed on its own through USB-C.

## Usage

Select **MiniCore → ATmega168** as the board, choose the CH340E COM port and upload as with any other Arduino.