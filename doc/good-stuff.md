# Good stuff

## Time of day binary sensor

Time of day platform [usage example](https://community.home-assistant.io/t/time-of-day-with-dual-input/393459/3)

## Outcast

Outcast [discussion](https://community.home-assistant.io/t/template-sensor-value-drops-to-0/254120)

## ESPHome

### CO2 and TVOC

Sensors [comparison](https://www.youtube.com/watch?v=FL0L-nic9Vw)

### CCS811 CO2/TVOC sensor

* [CCS811](https://www.sciosense.com/products/air-quality-sensors-environmental-sensors/ccs811/) is a digital gas sensor solution that integrates a metal oxide (MOX) gas sensor, an analog-to-digital converter (ADC), signal processing, and an I2C interface. It is designed to detect a wide range of Volatile Organic Compounds (VOCs) and Total Volatile Organic Compounds (TVOCs) in the air. The sensor is capable of detecting a wide range of VOCs, including alcohols, aldehydes, ketones, esters, aromatic and chlorinated hydrocarbons, and many more.
* [Datasheet](https://www.sciosense.com/wp-content/uploads/documents/SC-001232-DS-3-CCS811B-Datasheet-Revision-2.pdf)
* ESP8266 [wiring](https://www.youtube.com/watch?v=-91pz90qdos)

## Philips Hue White

[Reset](https://www.reddit.com/r/esp32/comments/drfn9u/how_to_reset_a_philips_hue_bulb_without_a_bridge/)

Start with light off for at least 5 seconds. Turn on for 8 seconds. Turn off for 2 seconds. Repeat this process 5 more times, or until the light bulb flashes. The light will flash 3 times if it has been successfully reset. 

## IKEA TRADFRI motion sensor E1525/E1745

[Buttons explanation](https://community.smartthings.com/t/tradfri-button-explanation-for-e1745-motion-sensor/222877/2)

* The sun/moon button is asking you whether you want it to work 24 hours a day, or only when it is dark.
* The other button ... is the dim setting you want the bulbs to use if you have the motion sensor directly controlling Tradfri bulbs. It is a choice between 30% bright setting or 100% bright setting.