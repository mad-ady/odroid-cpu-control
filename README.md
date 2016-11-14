# odroid-cpu-control
Simple script to set CPU parameters such as governor and frequencies for your Odroid device (C0, C1, C2, XU3, XU4, RPI, and basically linux device, even PC - sorry, the name is misleading)

Usage:
```
./odroid-cpu-control [options]

 -l, --list                 List a parameter
 -s, --set                  Set a parameter
 -g, --governor <governor>  Select a governor
 -c, --cpu <number|range>   The CPU to edit/query. Leave blank for all CPUs. Valid syntax:
                            0; 0,4; 0,4,5-7; 0-7
 -m, --min <number>         The minimum CPU frequency (must be supported by governor and CPU)
 -M, --max <number>         The maximum CPU frequency (must be supported by governor and CPU)
 -f, --frequency            The current CPU frequency
 -t, --temperature		        The current CPU temperature
 -q, --quiet                Don't display much output when setting a parameter
 -i, --interactive <number>	Keep running the list command every number seconds
 -h, --help                 Show this help screen
```
Examples:

* list current settings for all CPUs:
 <pre>./odroid-cpu-control -l</pre>
* list current settings for CPU 3:
 <pre>./odroid-cpu-control -l -c 3</pre>
* list current frequency for CPU 3:
 <pre>./odroid-cpu-control -l -c 3 -f</pre>
* list current governor for CPU 3:
 <pre>./odroid-cpu-control -l -c 3 -g</pre>
* set governor, min, max frequency for all CPUs:
 <pre>./odroid-cpu-control -s -g "powersave" -m 300M -M 1G</pre>
* set governor, min, max frequency for cpus 1, 4, 5 and 6:
 <pre>./odroid-cpu-control -s -g "powersave" -m 400M -M 1.3G -c 1,4-6</pre>

Installation:
The simplest way to install this is to download it to /usr/local/bin
```
wget https://raw.githubusercontent.com/mad-ady/odroid-cpu-control/master/odroid-cpu-control -O /usr/local/bin/odroid-cpu-control
chmod a+x /usr/local/bin/odroid-cpu-control
```

Persistence:
The best way to set the frequency/governor to be persistent on boot is to edit /etc/rc.local and add a call to odroid-cpu-control before exit 0. Example:

```
/usr/local/bin/odroid-cpu-control -s -g "conservative"
```
Also, please note that some distributions (Odroid included) have a script called /etc/init.d/ondemand which may set a different governor on boot. In order not to interfere with your setting, it's best to disable it:
```
sudo chmod a-x /etc/init.d/ondemand
```
