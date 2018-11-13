# freebsd-tools

This is a collection of utilities we use at Ping Pong AB for running, deploying and maintaining our FreeBSD systems.

## jail_autonet

Manage jails using netgraph and a VIMAGE enabled kernel.

## jail_and_zfsgptboot.diff
This patch adds a switch to get options out from jail.conf.

Use `jail -o` to get options from the /etc/jail.conf.
Also allow a bridge to be configured in the config file.
