# odroid-xu3-cpu-control
Simple script to set CPU parameters such as governor and frequencies for your XU3 (and possible XU4)

Usage:

./odroid-xu3-cpu-control [options]

Options:
 -l, --list                      List a parameter
 -s, --set                       Set a parameter
 -g, --governor <governor>       Select a governor (available in cpufreq-info)
 -c, --cpu <number>              The CPU to edit/query. Leave blank for all CPUs
 -m, --min <number>              The minimum CPU frequency (must be supported by governor and CPU. More info in cpufreq-info)
 -M, --max <number>              The maximum CPU frequency (must be supported by governor and CPU. More info in cpufreq-info)
 -f, --frequency                 The current CPU frequency
 -q, --quiet                     Don't display much output when setting a parameter
 -h, --help                      Show this help screen
 
Examples:

* list current settings for all CPUs:
 ./odroid-xu3-cpu-control -l
* list current settings for CPU 3:
 ./odroid-xu3-cpu-control -l -c 3
* list current frequency for CPU 3:
 ./odroid-xu3-cpu-control -l -c 3 -f
* list current governor for CPU 3:
 ./odroid-xu3-cpu-control -l -c 3 -g 0
* set governor, min, max frequency for all CPUs:
 ./odroid-xu3-cpu-control -s -g "conservative" -m 300 -M 1000

Bugs:
* When listing, parameters such as -m, -M, -g expect a value even if it's not used
* Setting runs internally sudo su -c even if the script is run as root. There's a problem running the command from inside the script - something different in the environment. If you run it as non-root with sudo and you want to run it non-interactivelly, it would help if it could configure sudo to authenticate your user without a password.
* Parameters are not validated. cpufreq-set/cpufreq-info will complain if you supply bad parameters.
