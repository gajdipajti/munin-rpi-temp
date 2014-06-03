munin-rpi-internal-temp
=======================

Check the [wiki page](https://github.com/gajdipajti/munin-rpi-temp/wiki) for results or the [blog post in hungarian](http://logout.hu/cikk/homerseklet_mero_pi/teljes.html)

Munin plugin for monitoring Raspberry Pi internal temperature: rpi-internal-temp

Munin plugin for monitoring a DS18B20 OneWire based temperature sensor connected to the Raspberry Pi: rpi-w1-temp

Munin plugin for monitoring temperature and humidity with an Aosong 2302, DHT11, DHT22 connected to the Raspberry Pi. This plugin uses the Adafruit binary from https://learn.adafruit.com/dht-humidity-sensing-on-raspberry-pi-with-gdocs-logging/software-install

Installation
------------

0. To use the OneWire sensor load kernel modules: w1-gpio w1-therm
You can add them also to /etc/modules

1. Copy the plugin files to /etc/munin/plugins

OR (cleaner)

1. Copy the plugin files to /usr/share/munin/plugins and link them

ln -sf /usr/share/munin/plugins/rpi-internal-temp /etc/munin/plugins/rpi-internal-temp

ln -sf /usr/share/munin/plugins/rpi-internal-freq /etc/munin/plugins/rpi-internal-freq

ln -sf /usr/share/munin/plugins/rpi-w1-temp /etc/munin/plugins/rpi-w1-temp

2. Reload munin-node

DHT sensors: munin will need root access: /etc/munin/plugin-conf.d/sensors

[rpi-dht-sensor_*]

user root

group root
