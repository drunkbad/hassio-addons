# SSH Tunnel

Hass.io addon for configuring external access to **Home Assistant** via an external server via SSH protocol. Useful if you have a "gray" IP address.

To work, you must already have a rented server with SSH access.

By default, the addon forwards ports 80 and 443 of the Hass.io server to an external server. It also creates a SOCKS proxy on the Hass.io server.

The first time you set it up, it's enough to configure the `host`, `port` and `user` of your server.

When run, the public SSH key (rather long) will be displayed in the logs, for example:

```
ssh-rsa AAAAB3NzaC1yc2EA...XfsAODObXZRVMI03 root@2fc7ce79c3de
```

The key is randomly generated every time the addon is installed. It must be **copied to your public server** in the home directory of the user on whose behalf you are connecting to the server via SSH:

`~/.ssh/authorized_keys`

For example `/root/.ssh/authorized_keys` or `/home/USERNAME/.ssh/authorized_keys`

If necessary, create a `.ssh` directory and an `authorized_keys` file - they may not be there.

**Warning!** The `.ssh` directory is considered hidden.

After a break - the connection will be restored automatically. But read the section **Discontinuity Recovery**.

## Settings

- `ssh_host` - public server address
- `ssh_user` - public server user
- `ssh_port` - public server port
- `tunnel_http` - redirect HTTP port
- `tunnel_https` - redirect HTTPS port
- `socks_port` - enable SOCKS proxy mode on the specified port of the Hass.io server
- `advanced` - additional ssh command parameters
- `before` - see section **Crash Recovery**

**Attention!** To forward "privileged" ports (for example, 80 and 443), the public server user must be an administrator. If you have problems with this, you can google: **ssh forward privileged ports**.

Config example:

- forwards ports 80 and 443 from the Hass.io server to an external server
- creates a SOCKS proxy on 
