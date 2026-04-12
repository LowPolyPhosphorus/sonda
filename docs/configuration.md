# Configuration

All configuration is done through `firmware/sonda.yaml` and `firmware/secrets.yaml`.

## secrets.yaml

| Key | Description |
|-----|-------------|
| `wifi_ssid` | Your WiFi network name |
| `wifi_password` | Your WiFi password |
| `api_encryption_key` | Base64 encryption key for Home Assistant API |
| `ota_password` | Password for over the air firmware updates |
| `fallback_password` | Password for the fallback hotspot if WiFi fails |

## GPIO Pins

| Pin | Function |
|-----|----------|
| GPIO21 | I2C SDA (BME280, BH1750) |
| GPIO22 | I2C SCL (BME280, BH1750) |
| GPIO18 | SPI CLK (GC9A01) |
| GPIO23 | SPI MOSI (GC9A01) |
| GPIO5 | GC9A01 CS |
| GPIO17 | GC9A01 DC |
| GPIO16 | GC9A01 RST |
| GPIO34 | Rain sensor analog input |
| GPIO35 | MQ-135 analog input |
| GPIO32 | MQ-2 analog input |

These can be changed in `sonda.yaml` if your wiring differs. Note that GPIO34 and GPIO35 are input only pins and cannot be used as outputs.

## Update Intervals

Sensors update on the following intervals by default:

| Sensor | Interval |
|--------|----------|
| BME280 | 30s |
| BH1750 | 30s |
| Rain sensor | 10s |
| MQ-135 | 30s |
| MQ-2 | 30s |

These can be changed by editing the `update_interval` field under each sensor in `sonda.yaml`. The rain sensor updates more frequently by default since rainfall is more time sensitive than the other readings.

## BME280 Address

The BME280 I2C address is set to `0x76` by default. If your module uses `0x77` instead change this line in `sonda.yaml`:

```yaml
address: 0x76
```

## Rain Sensor Threshold

The rain sensor outputs a percentage from 0 to 100 where 0 is completely dry and 100 is fully saturated. The raw ADC value is scaled to this range automatically. No threshold configuration is needed since Home Assistant automations can use any value range you define.

## MQ Sensor Warmup

The MQ-135 and MQ-2 sensors require approximately 30 seconds of warmup time after boot before their readings are accurate. Readings during this period should be ignored. Both sensors also require 5V on their VCC pin via the ESP32 VIN pin.

## Display

The GC9A01 display shows temperature, humidity, and pressure by default. To change what is displayed edit the lambda block under the display section in `sonda.yaml`.
