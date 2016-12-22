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

If you use multiple clients to connect to one server then check that you have autossh
with version >= 1.4a-1.

Ssh binds to a monitoring port on the remote machine. Before the mentioned version a fixed
port was used and multiple clients could not bind to the same port at the same time
which caused the ssh session to be restarted every 10 minutes. 

In later versions this is fixed by randomizing this port. If you still encounter problems
you can try setting the `ssh_tunnel_client_disable_monitoring` variable to true which basically
adds the `-M 0` option. 

Even without the monitoring it should work fine, because ssh exits quickly when there is no 
connection thanks to `-oServerAliveInterval=60 -oServerAliveCountMax=2` options. 

For more info see:
https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=351162