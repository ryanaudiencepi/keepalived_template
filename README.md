This example uses keepalived for 2 nginx load balancer servers running on active-passive failover.

## Keepalived on Centos
<pre>
yum -y install nginx
yum -y install gcc kernel-headers kernel-devel
yum -y install keepalived

echo "net.ipv4.ip_nonlocal_bind = 1" >> /etc/sysctl.conf
sysctl -p
</pre>

## Keepalived Configuration
On master server, upload keepalive-master.conf to /etc/keepalived/keepalived.conf  
On backup server, upload keepalive-backup.conf to /etc/keepalived/keepalived.conf  
Needless to say, you should use your own virtual ip address =)

<pre>
service keepalived start
chkconfig keepalived on
</pre>

## Keepalived Check
Keepalived output logs to syslog. Run "tail -f /var/log/messages" on both servers. 

- When you start the service your master server should transit to Master State and your backup server should transit to Backup state. 

- If you turn off your master server, backup server should transit to Master state.
 
- If master server goes back live backup server should be in Backup state.
