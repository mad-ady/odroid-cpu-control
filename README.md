# odroid-xu3-cpu-control
Simple script to set CPU parameters such as governor and frequencies for your XU3 (and possible XU4)

Usage:
```
./odroid-xu3-cpu-control [options]

 -l, --list                 List a parameter
 -s, --set                  Set a parameter
 -g, --governor <governor>  Select a governor
 -c, --cpu <number|range>   The CPU to edit/query. Leave blank for all CPUs. Valid syntax:
                            0; 0,4; 0,4,5-7; 0-7
 -m, --min <number>         The minimum CPU frequency (must be supported by governor and CPU)
 -M, --max <number>         The maximum CPU frequency (must be supported by governor and CPU)
 -f, --frequency            The current CPU frequency
 -q, --quiet                Don't display much output when setting a parameter
 -h, --help                 Show this help screen
```
Examples:

* list current settings for all CPUs:
 <pre>./odroid-xu3-cpu-control -l</pre>
* list current settings for CPU 3:
 <pre>./odroid-xu3-cpu-control -l -c 3</pre>
* list current frequency for CPU 3:
 <pre>./odroid-xu3-cpu-control -l -c 3 -f</pre>
* list current governor for CPU 3:
 <pre>./odroid-xu3-cpu-control -l -c 3 -g</pre>
* set governor, min, max frequency for all CPUs:
 <pre>./odroid-xu3-cpu-control -s -g "powersave" -m 300M -M 1G</pre>
* set governor, min, max frequency for cpus 1, 4, 5 and 6:
 <pre>./odroid-xu3-cpu-control -s -g "powersave" -m 400M -M 1.3G -c 1,4-6</pre>

