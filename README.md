# reverse-ssh-tunnel

Requires: `autossh`

Bash script to establish an automatic and permanent SSH tunnel with reversed port forwarding.

This allows connections to a remote (public) host to be forwarded to a host behind a NAT in the local network.  

Disconnections and re-connections will be gracefully handled by autossh. For this to work you should setup authentication using SSH keys.

It does the following:

1. Establishes an SSH connection to `REMOTE_HOST`;
2. binds `REMOTE_HOST_TUNNEL_PORT` in `REMOTE_HOST`;
3. forwards incoming connections from  
   `REMOTE_HOST`:`REMOTE_HOST_TUNNEL_PORT`  
   to  
   `LOCAL_HOST`:`LOCAL_HOST_TUNNEL_PORT`.

**Note:** In order to bind `REMOTE_HOST_TUNNEL_PORT` to all interfaces in `REMOTE_HOST`, you may need to add `'GatewayPorts yes'` to the sshd configuration of `REMOTE_HOST`. Remember to restart the sshd daemon after making changes to its configuration.  
Failing to do this may result in the tunnel refusing external connections.  

Also, `LOCAL_HOST` is relative to the host where you run this script from, and it can either be `localhost` itself, or any other host accessible by it.

Default configuration forwards `REMOTE_HOST`:`8888` to `LOCAL_HOST`:`80`.

Copyright (C) 2015-2018 Filipe Farinha - All Rights Reserved
Permission to copy and modify is granted under the GPLv3 license
