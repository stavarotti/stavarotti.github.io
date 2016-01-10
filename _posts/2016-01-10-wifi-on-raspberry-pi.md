---
layout: post
title: "Prevent Raspberry Pi Wi-Fi from Going into Power Saving Mode"
date: 2016-01-10 12:18:00
categories: raspberrypi
tags: raspberrypi, linux
---

After successfully setting up Wi-Fi on the Raspberry Pi, I noticed a repeated
pattern in which the connection dropped after several minutes of network
inactivity.

## Solution

It turns out the Wi-Fi module (8192cu) goes into power saving mode which
in-turn shuts down Wi-Fi network access.  To turn off Wi-Fi power saving, add
a configuration file (if absent) named `8192cu.conf` to `/etc/modprode.d`:

{% highlight bash linenos %}
$ cd /etc/modprobe.d
$ sudo touch 8192cu.conf
{% endhighlight %}

Now, using your preferred editor (nano is the default editor on Raspbian),
open the file for edit, and add the following configuration option:

{% highlight bash linenos %}
# Disable Wi-Fi power management
options 8192cu rtw_power_mgnt=0 rtw_enusbss=0
{% endhighlight %}

Save and reboot.  The Wi-Fi connection now stays up indefinitely.
