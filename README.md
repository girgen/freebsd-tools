# freebsd-tools

This is a collection of utilities we use at Ping Pong AB for running, deploying and maintaining our FreeBSD systems.

## jail_autonet

Manage jails using netgraph and a VIMAGE enabled kernel.

Drop this somewhere and point the rc_var `jail_program` to it. The jail is set up in `/etc/jail.conf` and it then expects all setting in the jail's /etc/rc.conf.

To get a complete jail this way, you need, of course, a complete install of FreeBSD for each jail, and also something along this example for `/etc/jail.conf` on the jail host.

```
# jail.conf
exec.start = "/bin/sh /etc/rc";
exec.stop = "/bin/sh /etc/rc.shutdown";
exec.clean;
mount.devfs;
mount.fdescfs;
allow.sysvipc;
devfs_ruleset=4;

allow.raw_sockets;

# Dynamic wildcard parameter:
# Base the path off the jail name.
path = "/jails/$name";
exec.consolelog = "/var/log/console.$name";

vnet = "new";
#no internal interface per default
#vnet.bridge=bxe0, bxe1; 

host.hostname = "$name.example.com";
#vnet.interface = ng0$name, ng1$name;

vnet.interface = ng0$name;
vnet.bridge = bxe1;

mount.fstab="/etc/fstab.$name";

porttest {
        vnet.bridge = bxe0;
}

```

## jail_and_zfsgptboot.diff
This patch adds a switch to get options out from jail.conf.

Use `jail -o` to get options from the /etc/jail.conf.
Also allow a bridge to be configured in the config file.
