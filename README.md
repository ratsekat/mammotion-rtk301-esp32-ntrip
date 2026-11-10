# Mammotion RTK301 → ESP32 → RTK2go

1. **Wire** verified 3.3 V UART out → ESP32-WROOM-32 GPIO16, with common GND. Leave ESP32 TX disconnected. Input: **460800 8N1**.
2. **Flash** `mammotion-xbee-flash.zip` using its `flash_args` for image offsets and settings.
3. **Configure** at [192.168.4.1](http://192.168.4.1) on the `ESP_XBee_…` hotspot. Set Wi-Fi Station and NTRIP Server to `rtk2go.com:2101` with your mountpoint and Rev1 source password. Save and reboot.

**Why custom firmware?** The RTK301’s Unicore UM960 UART mixes RTCM3 corrections with NMEA and other data. The ESP32 forwards only CRC-valid RTCM3 frames to RTK2go. The Mammotion firmware stays untouched.

**Observed RTK301 output:** MSM3 only for observations (`1073/1083/1093/1123`, every ~4 s), plus base position `1006` and receiver/antenna descriptor `1033` (~10 s). No MSM4 or `1230` seen.

Source: `mammotion-esp32-xbee-rtcm.zip` · ESP-IDF 4.4.8 · Based on [nebkat/esp32-xbee](https://github.com/nebkat/esp32-xbee), GPL-3.0.
