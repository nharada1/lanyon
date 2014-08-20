---
layout: post
title: Fixing low memory errors in Amazon EC2 (Ubuntu)
comments: True
---

Amazon's AWS offers a [free tier](http://aws.amazon.com/free/) that provides a year's worth of a [micro instance](http://aws.amazon.com/ec2/instance-types/) along with a decent amount of storage and other services. If you use an EBS volume for your instance you can easily upgrade your machine to more powerful instances for cheap. For the most part, the micro instance is plenty of power for basic development I do. However, occasionally I'll need an extra boost. Most recently I ran into problems running `cabal update` during my Haskell learning adventures.

Sometimes a process will terminate for no reason - especially during compilation. If this happens to you, run `dmesg` and check for an "Out of Memory" error.

While you could shutdown the instance and upgrade to a larger version (for a price), an easier way is to temporarily add swap space. When a computer doesn't have enough physical RAM, it can use swap space as virtual memory. While slower than hardware, this space lets you increase the physical memory seen by the machine.

Without further ado, let's add some swap space:

First check to see if you have any swap space in the first place

`sudo swapon -s`

If you have no swap (as Ubuntu EC2 doesn't), you should see an empty list

`Filename                Type        Size    Used    Priority`

Next double check your disk usage. The swap file is hard disk space, and if you don't have enough this won't work. Run `df -h` to get a human readable output.

{% highlight bash %}
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1      7.8G  5.2G  2.2G  71% /
none            4.0K     0  4.0K   0% /sys/fs/cgroup
udev            283M   12K  283M   1% /dev
tmpfs            59M  656K   59M   2% /run
none            5.0M     0  5.0M   0% /run/lock
none            295M     0  295M   0% /run/shm
none            100M  4.0K  100M   1% /run/user
{% endhighlight %}

We have plenty of space available. We'll add a 256K swap partition, which will increase our memory by 50%. 

{% highlight bash %}
sudo dd if=/dev/zero of=/swapfile bs=1024 count=256k
sudo mkswap /swapfile
sudo swapon /swapfile
{% endhighlight %}

If all goes according to plan you should be able to see the swap partition by running `swapon -s`

{% highlight bash %}
Filename                Type        Size    Used    Priority
/swapfile                               file        262140  0   -1
{% endhighlight %}

This file will disappear on reboot, making it good for when you need to run big jobs infrequently. If you want to make this swap permanent you can follow instructions at [this DigitalOcean post](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-12-04). 
