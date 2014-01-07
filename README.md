munin-rpi-internal-temp
=======================

Check the wiki page for results or the [blog post in hungarian](http://logout.hu/cikk/homerseklet_mero_pi/teljes.html)

Munin plugin for monitoring Raspberry Pi internal temperature: rpi-internal-temp

Munin plugin for monitoring a DS18B20 OneWire based temperature sensor connected to the Raspberry Pi: rpi-w1-temp

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

