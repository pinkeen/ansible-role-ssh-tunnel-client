# Create persistent ssh tunnels via autossh (Centos7)

`ssh_tunnel_client_user` - default is `ssh_tunnel` 

`ssh_tunnels` - array with keys:
 - `name` - name used for naming services
 - `key_file` - priv ssh key
 - `target_host` - required
 - `target_port` - required
 - `local_port` - required
 - `remote_user` - set to `ssh_tunnel` by default