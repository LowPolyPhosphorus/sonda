# Installation

## Requirements

- ESP32-WROOM
- ESPHome CLI
- Home Assistant with ESPHome integration
- Python 3.x
- HACS with Mushroom Cards installed in Home Assistant

## Installing ESPHome

Open PowerShell and run:

```powershell
pip install esphome
```

## Installing Mushroom Cards

1. Install HACS in Home Assistant if not already installed
2. Go to HACS > Frontend > Search "Mushroom"
3. Install Mushroom and restart Home Assistant

## Setting Up Files

1. Clone the repo
2. Copy `firmware/secrets.yaml.example` to `firmware/secrets.yaml`
3. Fill in your WiFi credentials and generate an API encryption key by running this in PowerShell:

```powershell
[Convert]::ToBase64String((1..32 | ForEach-Object { [byte](Get-Random -Max 256) }))
```

4. Copy the output into the `api_encryption_key` field in `secrets.yaml`

## Flashing

1. Place your firmware folder somewhere with no spaces in the path, for example `C:\sonda\firmware`
2. Set PlatformIO to use a path with no spaces by running this in PowerShell:

```powershell
[System.Environment]::SetEnvironmentVariable("PLATFORMIO_CORE_DIR", "C:\pio", "User")
```

3. Close and reopen PowerShell
4. Run:

```powershell
esphome run "C:\sonda\firmware\sonda.yaml"
```

5. Select your COM port when prompted

## Home Assistant

Once flashed and on your network, Home Assistant will autodiscover Sonda automatically. Go to Settings > Devices & Services and accept the ESPHome notification. Enter your API encryption key from secrets.yaml when prompted.

## Notes

- PlatformIO cannot handle spaces in file paths on Windows, keep the firmware folder at a path with no spaces
- GPIO35 and GPIO34 are input only pins on the ESP32, do not try to use them as outputs
- MQ-135 and MQ-2 require 5V on their VCC pin, not 3.3V, use the VIN pin on the ESP32 which passes through USB 5V directly
- The MQ sensors require a warmup period of about 30 seconds after boot before readings are accurate
