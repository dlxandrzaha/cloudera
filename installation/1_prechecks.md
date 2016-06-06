
# <center> Configuration Checks
## <center> Swappiness
* Check current swappiness
<code>$ </code>
<code>$ 30</code>

* Change swappiness
<code>$ echo 1 > /proc/sys/vm/swappiness</code>

* Set persist on reboot
<code>$ echo "vm.swappiness = 1" >> /etc/sysctl.conf</code>

* Check new swappiness
<code>$ cat /proc/sys/vm/swappiness</code>
<code>$ 1</code>

**Note:** The same command was executed as one on all other nodes.
Example: `$ echo 1 > /proc/sys/vm/swappiness && echo "vm.swappiness = 1" >> /etc/sysctl.conf && cat /proc/sys/vm/swappiness`

## <center> File access time (noatime)
**Note:** Only updated on worker nodes
