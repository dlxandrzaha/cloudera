
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
**Issue:** Had to add second volumes on worker nodes as on AWS that was used there was a single volumne with XFS file system and limited space. By adding a second volume it was easy to format it in ext4 file format.

## <center> SELinux
* Disabled SELinux on all servers (on boot)
<code>$ /etc/selinux/config</code>
* Disable SELinux immediately
<code>$ setenforce 0</code>

## <center> Transparent Hugepages
* Check Transparent Hugepages current status
<code>$ cat /sys/kernel/mm/transparent_hugepage/enabled</code>
<code>[always] madvise never</code>

**Note:** Used to be "redhat_transparent_hugepage". In RHEL 7.2 it's "transparent_hugepage"
* Set transparent hugepage on boot using script
```$ if test -f /sys/kernel/mm/transparent_hugepage/enabled; then
   echo never > /sys/kernel/mm/transparent_hugepage/enabled
fi```
* Change Transparent Hugepages without reboot
<code>$ echo never > /sys/kernel/mm/transparent_hugepage/enabled</code>
* Check Transparent Hugepages current status
<code>$ cat /sys/kernel/mm/transparent_hugepage/enabled</code>
<code>always madvise [never]</code>

## <center> Name Service Cashe Daemon (nscd)
* Had to install the service
`$ yum install nscd`
* Had to modify the config for nscd (RHEL 7.2)
`$ vi /etc/nscd.conf
* Settings used:
	* enable-cache hosts yes
	* enable-cache passwd no
	* enable-cache group no
	* enable-cache netgroup no
* Enabled nscd
`chkconfig --level 345 nscd on`
* Started the service
`service nscd start`

## <center> DNS
* Installed bind utils
`$ yum install bind-utils`
* Public DNS
`$ host ec2-52-208-1-52.eu-west-1.compute.amazonaws.com`
`ec2-52-208-1-52.eu-west-1.compute.amazonaws.com has address 172.31.34.101`
* Private DNS
`$ host ip-172-31-34-101.eu-west-1.compute.internal`
`ip-172-31-34-101.eu-west-1.compute.internal has address 172.31.34.101`
* Public IP
`$ host 52.208.1.52`
`52.1.208.52.in-addr.arpa domain name pointer ec2-52-208-1-52.eu-west-1.compute.amazonaws.com.`
* Private IP
`$ host 172.31.34.101`
`101.34.31.172.in-addr.arpa domain name pointer ip-172-31-34-101.eu-west-1.compute.internal.`

## <center> NTP
**Note:** Skipped all machines running on EU (Ireland) - AWS. No issues expected. If issues happen NPT will be setup later.
