# susv_munin_plugin
## What it does

A Munin plugin for monitoring the [susv](http://www.s-usv.de/index_en.php)

This plugin fetches the voltage and current from input and battery and the battery capacity and visualizes them in munin graphs.

I put this together without knowing a thing about python programming or munin plugin programming so keep that in mind when you stumble over the numerous errors and design mistakes I've certainly made ;)

## How to install

First you should clone the repository with
`git clone https://github.com/TWfromSWD/susv_munin_plugin.git`
You'll end up with directory called susv_munin_plugin containing this file and the plugin Python script named `susv_`
For the plugin to work you'll need python and the [susv client software](http://www.s-usv.de/downloads_en.html) installed.

The Plugin needs to be copied into the munin plugin directory which should be
`/usr/share/munin/plugins/`
on the Raspberry Pi.

Also the plugin's configuration needs to be added to
`/etc/munin/plugin-conf.d/munin-node`
```
[susv*]
user root
group root
```

This plugin is enabled for automatic installation by munin-node-configure so after you followed the above steps you just need to run
`sudo munin-node-configure --shell` to get the shell code for creating the needed symlinks. Or you can just pipe that output directly to the shell by running
`sudo /usr/sbin/munin-node-configure --shell | sudo sh` in the `/etc/munin/plugins` directory.

Either way you should end up with this additional symlinks:
```
lrwxrwxrwx 1 root root 30 Apr 17 14:03 susv_battery -> /usr/share/munin/plugins/susv_
lrwxrwxrwx 1 root root 30 Apr 17 14:03 susv_currents -> /usr/share/munin/plugins/susv_
lrwxrwxrwx 1 root root 30 Apr 17 14:03 susv_voltages -> /usr/share/munin/plugins/susv_
```
Now you just need to restart the munin-node by typing
`sudo service munin-node restart`
and the graphs should start showing up in the next cycle.
