# Setup mosquitto on Ubuntu Core

Raspberry Pi v3 with Ubuntu Core 20 will be used

1. Install Mosquitto on Rpi and on main machine

```bash
sudo snap install mosquitto
```

2. Create new config file for moquitto

```bash
touch /var/snap/mosquitto/common/mosquitto.conf
vi /var/snap/mosquitto/common/mosquitto.conf

/* Enter the following */

allow_anonymous true
listener 1883
listener 8883
listener 8083
protocol websockets
```

3. Restart mosquitto service on RPi using systemctl

```bash
sudo systemctl restart snap.mosquitto.mosquitto.service
```

4. Check logs

```bash
sudo journalctl -f -u snap.mosquitto.mosquitto.service
```

5. On main machine subscribe to topic "test"

```bash
mosquitto_sub -t test
```

6. Publish message on Rpi to main machine on topic "test"

```bash
mosquitto_pub -h TARGET_IP -t test -m rpi
```

7. Check terminal for message where step 5. was run
