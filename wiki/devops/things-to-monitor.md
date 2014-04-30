(Based largely on http://word.bitly.com/post/74839060954/ten-things-to-monitor?h=2)

* rate of new process creation (`fork()` rate)
* flow control packets
* swap rate
* (unexpected) system reboots
* clock accuracy/skew
  * ensure that ntpd is running
* whether your SSL certificates are still valid (haven't expired yet)
* number of open file descriptors vs. the configured fd limit
* number of open connections of server application (e.g. MySQL) vs. configured connection limit
* service restart rate (assuming auto-restart is setup)
* DNS
  * whether external users can resolve your domains
  * perf stats on your internal DNS servers
  * whether your upstream DNS server is working
* DB slave replication status
* the obvious ones: CPU, RAM, disk space
* max subdirectories in a single directory (Ext3 w/o dir_index has a limit of 32K subdirs)
* free inodes per filesystem
* number of cgroups
