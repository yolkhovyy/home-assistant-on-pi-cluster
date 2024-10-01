# Zigbee2MQTT

Zigbee2MQTT [License](https://github.com/Koenkk/zigbee2mqtt/blob/master/LICENSE)

CC2531 coordinator hardware installation see in [hardware.md](hardware.md#zigbee).

See [docker-compose.yml](../zigbee2mqtt/docker-compose.yml).

```bash
cd zigbee2mqtt/
docker compose up -d
```

## Flashing SONOFF Zigbee Dongle-P

```bash
# Get the coordinator firmware
git clone https://github.com/Koenkk/Z-Stack-firmware.git
cd Z-Stack-firmware/coordinator/Z-Stack_3.x.0/bin/
unzip CC1352P2_CC2652P_launchpad_coordinator_20240710.zip
mv CC1352P2_CC2652P_launchpad_coordinator_20240710.hex your/location/

# Open the dongle, press the boot mode button. connect to USB
# See https://www.youtube.com/watch?v=KBAGWBWBATg
# Check it's connected
ls -l /dev/ttyUSB0

# Flashing
cd your/location/
wget https://github.com/JelmerT/cc2538-bsl/raw/master/cc2538-bsl.py
sudo pip3 install intelhex pyserial
sudo python3 ../cc2538-bsl.py -p /dev/ttyUSB0 -evw CC1352P2_CC2652P_launchpad_coordinator_20240710.hex

# Reconnect the dongle without pressing the boot mode button
# Check it's connected
ls -l /dev/ttyUSB0
```bash

## Zigbee2MQTT Configuration

```bash
cd zigbee2mqtt/
nano data/configuration.yaml 
```

**data/configuration.yaml**

```yaml
serial:
  port: /dev/ttyUSB0
```

**docker-compose.yaml**

```yaml
services:
  zigbee2mqtt:
    container_name: zigbee2mqtt
    image: koenkk/zigbee2mqtt:1.30.4
    restart: unless-stopped
    network_mode: host
    volumes:
      - ./data:/app/data
      - /run/udev:/run/udev:ro
    environment:
      - TZ=Europe/Amsterdam
    devices:
      # Make sure this matches your adapter location
      - /dev/ttyUSB0:/dev/ttyUSB0
```

Note: With the original firmware version (Before flashing the CC1352P2_CC2652P_launchpad_coordinator_20240710.hex firmware) the dongle connected as /dev/ttyACM0. After flashing the firmware, it connects as /dev/ttyUSB0.
