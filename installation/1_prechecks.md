
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
* Edit fstab
`$ vi /etc/fstab`
```
#
# /etc/fstab
#
# /etc/fstab
# Created by anaconda on Mon Nov  9 20:20:10 2015
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=379de64d-ea11-4f5b-ae6a-0aa50ff7b24d /                       xfs     defaults,noatime        0 0
```
* Apply
`mount -o remount /`

## <center> SELinux
* Disabled SELinux on all servers (on boot)
<code>$ vi /etc/selinux/config</code>
```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```
* Disable SELinux immediately
<code>$ setenforce 0</code>

## <center> Transparent Hugepages
* Check Transparent Hugepages current status
<code>$ cat /sys/kernel/mm/transparent_hugepage/enabled</code>
<code>[always] madvise never</code>

**Note:** Used to be "redhat_transparent_hugepage". In RHEL 7.2 it's "transparent_hugepage"
* Edit /etc/rc.local
`$ vi /etc/rc.local`
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
`$ yum install nscd -y`
* Had to modify the config for nscd (RHEL 7.2)
`$ vi /etc/nscd.conf
* Settings used:
	* enable-cache hosts yes
	* enable-cache passwd no
	* enable-cache group no
	* enable-cache netgroup no
* Enabled nscd
`$ chkconfig --level 345 nscd on`
```
Created symlink from /etc/systemd/system/multi-user.target.wants/nscd.service to /usr/lib/systemd/system/nscd.service.
Created symlink from /etc/systemd/system/sockets.target.wants/nscd.socket to /usr/lib/systemd/system/nscd.socket.
```
* Started the service
`$ service nscd start`

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

**Note:** The process was repeaded on all other nodes

## <center> NTP
**Note:** Skipped all machines running on EU (Ireland) - AWS. No issues expected. If issues happen NPT will be setup later.
