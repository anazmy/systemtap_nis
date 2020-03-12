* On dev server compile the systemtap script
~~~
# stap -k -p4 nis_trace.stp -m nis_trace
nis_trace.ko
Keeping temporary directory "/tmp/stap7WVxJj"
~~~

* Copy these files to production servers
~~~
# scp /tmp/stap7WVxJj/uprobes/uprobes.ko nis_trace.ko <production_server>:
~~~

* deploy the module on production servers
~~~
# insmod uprobes.ko 
# staprun -o id_stap_$(hostname -s)_$(date +%Y%m%d-%H%M%S).log nis_trace.ko
~~~

* Once done testing, remove the probes kernel module from production servers
~~~
# rmmod uprobes
~~~
