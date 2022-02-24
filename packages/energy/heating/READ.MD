# Energy

## Heating

### Boiler control

Our boiler is a Viessmann with basis ON/OFF control. To control it following is used:

- ESP32
- 4-relay board
- 2 x 1-wire DS18B20 to measure heating pipe temperature
- 5V DC power supply


### Radiator control
Our house is still heated by a traditional gasoil boiler and high temperature radiators.
When we got the house there was only one thermostat. It was my goal to have room dependent heating.
To enable it without replacing the boiler we did the following:

- run wire to each radiator
- replace the existing manual thermostatic valves by 24V valves
- create 2 radiator controllers (one for each side of the house)
    - 24V DC power supply
    - ESP32
    - 8 relayboard
    - 2 x 1-wire DS18B20 to measure heating pipe temperature
    - esphome based firmware

Radiator relays are grouped so when one radiator asks for heating (See Thermostats) the group will go to state "On" which triggers the boiler through an automation.

### Temperature monitoring
Each room has minimum one temperature and humidity sensor.
As I have many rooms, I choose to go with the XIAOMI LYWSD03MMC as they are pretty cheap and they kind of look nice.
These are BLE sensors so I needed several BLE receiver in the house.
Each room or area has a vanilla ESP32 board to sense for BLE packets using esphome as firmware.
As the LYWSD03MMC has proprietary firmware, I flashed them with alterative firmware ATC_MiThermometer (https://github.com/pvvx/ATC_MiThermometer)


### Thermostats
For each room I defined a thermostat using the [Home Assistant Generic Thermostat](https://www.home-assistant.io/integrations/generic_thermostat/).