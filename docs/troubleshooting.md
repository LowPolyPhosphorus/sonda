# Troubleshooting

## ESPHome won't compile

Make sure your firmware folder and PlatformIO core directory are both at paths with no spaces. Move the firmware folder to somewhere like `C:\sonda\firmware` and run this in PowerShell to fix PlatformIO:

```powershell
[System.Environment]::SetEnvironmentVariable("PLATFORMIO_CORE_DIR", "C:\pio", "User")
```

Close and reopen PowerShell then try again.

## Home Assistant won't discover Sonda

Make sure Sonda and your Home Assistant server are on the same WiFi network. If autodiscovery does not work go to Settings > Devices & Services > Add Integration and search for ESPHome manually. Enter the IP address of Sonda when prompted.

## BME280 not showing up

Check the I2C address. Some BME280 modules use `0x77` instead of `0x76`. Change the address in `sonda.yaml` and reflash. You can also enable I2C scan in the logger to see what address your module is reporting.

## MQ sensors showing weird readings

The MQ-135 and MQ-2 need about 30 seconds to warm up after boot. Ignore readings during this period. Also make sure both sensors are connected to the VIN pin for 5V and not the 3V3 pin, they will not work correctly at 3.3V.

## Rain sensor always reading 0 or 100

Check that the sensor is connected to GPIO34 and that the AO pin is used and not the DO pin. The DO pin is digital only and will only output 0 or 1. The AO pin gives the full analog range.

## Display not showing anything

Check all five display connections, RST, CS, DC, SDA, and SCL. A missing RST or CS connection is the most common cause of a blank display. Make sure RST is on GPIO16, CS on GPIO5, DC on GPIO17, SDA on GPIO23, and SCL on GPIO18.

## Sonda keeps rebooting

Check your power supply. The ESP32 plus all six modules draws more current than some USB ports or cheap cables can provide. Use a quality USB power adapter rated for at least 1A.

## WiFi keeps disconnecting

If Sonda is far from your router the fallback hotspot will activate automatically. Connect to the fallback hotspot named "sonda fallback" and use the captive portal to reconfigure WiFi if needed.
