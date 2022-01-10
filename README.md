
[![Arduino CI](https://github.com/RobTillaart/MCP23S08/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![Arduino-lint](https://github.com/RobTillaart/MCP23S08/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/MCP23S08/actions/workflows/arduino-lint.yml)
[![JSON check](https://github.com/RobTillaart/MCP23S08/actions/workflows/jsoncheck.yml/badge.svg)](https://github.com/RobTillaart/MCP23S08/actions/workflows/jsoncheck.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/MCP23S08/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/MCP23S08.svg?maxAge=3600)](https://github.com/RobTillaart/MCP23S08/releases)


# MCP23S08

Arduino library for MCP23S08 8 channel SPI port expander.


## Description

This experimental library gives easy control over the 8 pins of a (SPI) MCP23S08 chip.

This IC is strongly related to the MCP23017 I2C port expander - https://github.com/RobTillaart/MCP23017_RT
Programming Interface is kept the same as much as possible.


## Interface

### Constructor

- **MCP23S08(uint8_t select, uint8_t data, uint8_t clock)** constructor SW SPI.
- **MCP23S08(uint8_t select)** constructor HW SPI.
- **bool begin()** returns true if successful.
- **bool isConnected()** returns true if connected, false otherwise. (dummy)


### Single pin interface

- **bool pinMode(uint8_t pin, uint8_t mode)** pin = 0..15, mode = INPUT, OUTPUT, returns true if successful.
- **bool digitalWrite(uint8_t pin, uint8_t value)** pin = 0..15, value = LOW(0) HIGH (!0), returns true if successful.
- **uint8_t digitalRead(uint8_t pin)** pin = 0..15, returns LOW or HIGH, might set the lastError();
- **bool setPolarity(uint8_t pin, bool reversed)** pin = 0..15, set reversed flag, returns true if successful.
- **bool getPolarity(uint8_t pin, bool &reversed)** pin = 0..15, reads reversed flag, returns true if successful.
- **bool setPullup(uint8_t pin, bool pullup)** pin = 0..15, set pull-up flag, returns true if successful.
- **bool getPullup(uint8_t pin, bool &pullup)** pin = 0..15, reads pull-up flag, returns true if successful.


### 8 pins interface

- **bool pinMode8(uint8_t port, uint8_t value)** port = 0..1, value = 0..255, returns true if successful.
- **bool write8(uint8_t port, uint8_t value)** port = 0..1, value = 0..255, returns true if successful.
- **uint8_t read8(uint8_t port)** port = 0..1, reads 8 pins into one byte.
- **bool setPolarity8(uint8_t port, uint8_t mask)** port = 0..1, sets polarity for 8 channels at once.
- **bool getPolarity8(uint8_t port, uint8_t &mask)** port = 0..1, reads polarity of 8 channels at once.
- **bool setPullup8(uint8_t port, uint8_t mask)** port = 0..1, sets pull-up for 8 channels at once.
- **bool getPullup8(uint8_t port, uint8_t &mask)** port = 0..1, reads pull-up for 8 channels at once.


### Error codes

- **int lastError()** Above functions set an error flag that can be read with this function.  
Reading it will reset the flag to **MCP23S08_OK**.

| DESCRIPTION           | VALUE |
|:----------------------|:-----:|
| MCP23S08_OK           |  0x00 |
| MCP23S08_PIN_ERROR    |  0x81 |
| MCP23S08_I2C_ERROR    |  0x82 |
| MCP23S08_VALUE_ERROR  |  0x83 |
| MCP23S08_PORT_ERROR   |  0x84 |


## Operation

See examples.


## Future

- keep functional in sync with MCP23017_RT
- **isConnected()** is not really needed
