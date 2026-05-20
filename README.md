# ESP32-S3 USB MSC SD Bridge

ESP32-S3 firmware that exposes an SPI-connected SD card as a USB Mass Storage device. The host sees a standard removable drive. I built this to flash an rpi.

Built with ESP-IDF 5.x and TinyUSB. The S3's internal USB-OTG controller handles enumeration; raw block reads/writes are forwarded to the SD card via `sdmmc_read_sectors` / `sdmmc_write_sectors` over SPI.

## Wiring

| SD module | ESP32-S3 |
|-----------|----------|
| CS        | GPIO10   |
| SCK       | GPIO12   |
| MOSI      | GPIO11   |
| MISO      | GPIO13   |
| VCC       | 3.3V     |
| GND       | GND      |

## Build

```bash
idf.py set-target esp32s3
idf.py build
idf.py -p /dev/ttyUSB0 flash
```

Flash via UART, then connect the USB-OTG port to the host.
