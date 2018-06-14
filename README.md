munin-rpi-internal-temp
=======================

Check the [wiki page](https://github.com/gajdipajti/munin-rpi-temp/wiki) for results or the [blog post in hungarian](http://logout.hu/cikk/homerseklet_mero_pi/teljes.html)

Munin plugin for monitoring Raspberry Pi internal temperature: rpi-internal-temp

Munin plugin for monitoring a DS18B20 OneWire based temperature sensor connected to the Raspberry Pi: rpi-w1-temp

Munin plugin for monitoring temperature and humidity with an Aosong 2302, DHT11, DHT22 connected to the Raspberry Pi. This plugin uses the Adafruit binary from https://github.com/adafruit/Adafruit_Python_DHT

If you use the code
------------

Please give me a star, because it is a good feeling that I helped someone. :)

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


2. Set the plugins executable

chmod a+x /usr/share/munin/plugins/rpi-internal-temp

chmod a+x /usr/share/munin/plugins/rpi-internal-freq

chmod a+x /usr/share/munin/plugins/rpi-w1-temp


3. Reload munin-node

Monitor hotspot
---------------

Use the rpi-hotspot-wlan0 script, tested on the OrangePi Zero.

DHT sensors
-----------

Do the Adafruit setup and copy the AdafruitDHT.py to /usr/local/bin
Give exec permission: sudo chmod +x /usr/local/bin/Adafruit.py

Munin plugins not working
-------------------------

munin will need root access: /etc/munin/plugin-conf.d/rpi

[rpi-*]

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
