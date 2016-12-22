# Create persistent ssh tunnels via autossh (Centos7)

`ssh_tunnel_client_user` - default is `ssh_tunnel` 

`ssh_tunnels` - array with keys:
 - `name` - name used for naming services
 - `key_file` - priv ssh key
 - `target_host` - required
 - `target_port` - required
 - `local_port` - required
 - `remote_user` - set to `ssh_tunnel` by default
 - `alive_interval` - set to `10` by default
 - `alive_count_max` - set to `1` by default
 
 
## Warning

Autossh binds to a monitoring port on the remote machine. A fixed port is used and multiple 
clients cannot not bind to the same port at the same time what causes the ssh session to be restarted 
every 10 minutes. 

The port randomization does not work in latest centos 7 version (1.4e) as of this writing.

That's why the autossh monitoring is turned off.

Even without the monitoring it should work fine, because ssh exits quickly when there is no 
connection thanks to `-oServerAliveInterval=60 -oServerAliveCountMax=2` options. 

For more info see:
https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=351162


Sidenote: Upon consideration, why do I need autossh then? Won't systemd take care of the restarting?