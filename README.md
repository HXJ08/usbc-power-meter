# USB-C Power Meter

A small board that sits between a USB-C charger and a device, showing real-time voltage and current on an OLED display.

## What it does

- Measures voltage (0-20V) and current (0-5A) over USB-C
- Displays readings on a 0.96" OLED (SSD1306, I2C)
- Updates display at 10Hz
- Powered from the USB-C VBUS line

## Parts

| Part | Qty | Cost | Source |
|---|---|---|---|
| Arduino Pro Micro (ATmega32U4) | 1 | $5 | Amazon/AliExpress |
| 0.96" OLED (SSD1306, I2C) | 1 | $4 | Amazon |
| INA219 current sensor breakout | 1 | $3 | Amazon/Adafruit |
| USB-C connector (SMD) | 1 | $2 | LCSC |
| PCB | 1 | $5 | JLCPCB |
| **Total** | | **~$19** | |

## Pinout

| Component | Pin |
|---|---|
| INA219 SDA | D2 (A4 on Pro Micro) |
| INA219 SCL | D3 (A5 on Pro Micro) |
| OLED SDA | D2 (shared I2C bus) |
| OLED SCL | D3 (shared I2C bus) |
| USB-C VBUS | VCC (through voltage divider) |
| USB-C CC1/CC2 | 5.1kΩ pull-down to GND (for UFP) |

## How it works

The INA219 is a high-side current sense amplifier with an I2C interface. It measures voltage across a shunt resistor and outputs both voltage and current over I2C. The Pro Micro reads the INA219 and displays the values on the OLED.

The USB-C connector needs 5.1kΩ pull-down resistors on CC1 and CC2 to advertise itself as a UFP (device), which tells the charger to supply power.

## Firmware

Uses `Wire.h` for I2C, `Adafruit_SSD1306` for the display, and `Adafruit_INA219` for the sensor. Reads voltage and current in a loop and updates the display.

## References

- [INA219 datasheet](https://www.ti.com/product/INA219)
- [USB-C CC pin configuration](https://www.ti.com/lit/an/slvaf83b/slvaf83b.pdf)
- [Adafruit INA219 guide](https://learn.adafruit.com/adafruit-ina219-current-sensor-breakout)

## License

MIT
