![Sonda](images/sonda.png)

An outdoor weather station built on ESP32 and ESPHome that monitors temperature, humidity, atmospheric pressure, light intensity, rainfall, air quality, and wildfire smoke, reporting all data locally to Home Assistant with zero cloud dependency.

## Features

- Temperature, humidity, and atmospheric pressure via BME280
- Light intensity via BH1750
- Rainfall detection via rain sensor module
- Air quality monitoring via MQ-135
- Wildfire smoke detection via MQ-2
- Live sensor readings displayed on a 1.28 inch GC9A01 round TFT display
- Full Home Assistant integration via ESPHome
- No cloud dependency, fully local

## Hardware

- ESP32-WROOM
- BME280 temperature, humidity, pressure sensor
- BH1750 light intensity sensor
- Rain sensor module
- MQ-135 air quality sensor
- MQ-2 smoke sensor
- GC9A01 1.28 inch round TFT display

## Wiring

See [wiring diagram](docs/wiring.txt) for full pin connections.

## Setup

See [installation guide](docs/installation.md) for flashing and Home Assistant setup instructions.

## Photos

Coming soon.
