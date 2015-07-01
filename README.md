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

DHT sensors
-----------

copy the bin folder content to /usr/local/bin

munin will need root access: /etc/munin/plugin-conf.d/sensors

[rpi-dht-sensor_*]

user root

group root

Kernel 3.18.* PROBLEM
---------------------

The new Raspberry Pi kernel has switched to device trees, this will break the w1 module.
[link](http://www.raspberrypi.org/forums/viewtopic.php?p=675658#p675658)
[link](http://raspberrypi.stackexchange.com/questions/27073/firmware-3-18-x-breaks-i2c-spi-audio-lirc-1-wire-e-g-dev-i2c-1-no-such-f)
[link](https://github.com/raspberrypi/firmware/issues/348)

Kernel 3.18.* FIX
-----------------

Add the following lines to the end of /boot/config.txt

    # 1-wire device tree
    dtoverlay=w1-gpio,gpiopin=4

Kernel 4.0.* DHT11 overlay
--------------------------

The current code is not compatible with the DHT11 overlay. I experimented with it, but 3 out of 5 reads have failed. [link](https://github.com/raspberrypi/linux/pull/1017)
Just keep using the adafruit code.