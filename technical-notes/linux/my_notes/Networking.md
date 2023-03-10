# Debian

[](https://askubuntu.com/posts/1321815/timeline)

On a typical Debian-based distribution you have two command-line utilities used to configure network interfaces: the deprecated [`ifconfig`](https://manpages.debian.org/stretch/net-tools/ifconfig.8.fr.html) from [`net-tools`](https://packages.debian.org/stretch/net-tools) and the newer [`ip`](https://manpages.debian.org/stretch/iproute2/ip.8.en.html) from [`iproute2`](https://packages.debian.org/stretch/iproute2).

However these two utilities directly configure the kernel and do not persist your config, if you reboot your machine you will need to reconfigure your interfaces again.

You have three major packages available for that purpose:

-   [`ifupdown`](https://packages.debian.org/stretch/ifupdown)
-   [`NetworkManager`](https://packages.debian.org/stretch/network-manager)
-   [`systemd`](https://packages.debian.org/stretch/systemd) and its daemon `systemd-networkd`

In general, you should choose one and stick to it, even if `ifupdown` works well with `NetworkManager` it can still creates unexpected configuration issues.

## ifupdown
Quite deprecated but reliable, you might encounter it on many older systems. The config is stored in `/etc/network/interfaces` and managed by the `networking.service` daemon which is a wrapper around the [`ifup`](https://manpages.debian.org/stretch/ifupdown/ifup.8.en.html) and [`ifdown`](https://manpages.debian.org/stretch/ifupdown/ifdown.8.en.html) commands which are also wrappers themselves around `ifconfig` (or `ip` for [`ifupdown2`](https://packages.debian.org/stretch/ifupdown2)).

Read the man at [`ifupdown`](https://manpages.debian.org/stretch/ifupdown/interfaces.5.en.html).

## NetworkManager
Usually included with desktop distributions since many graphical front-ends are available, the config is stored in `/etc/NetworkManager` and managed by the `NetworkManager.service` daemon.

You can manage the config with the included [`nmcli`](https://manpages.debian.org/stretch/network-manager/nmcli.1.en.html) or [`nmtui`](https://manpages.debian.org/stretch/network-manager/nmtui.1.en.html) utilities.

Read the man at [`NetworkManager`](https://manpages.debian.org/stretch/network-manager/NetworkManager.8.en.html).

## systemd-networkd
Usually used on server distributions and the official successor to `ifupdown` as it is included within `systemd`, the config is stored in `/etc/systemd/network` and managed by the `systemd-networkd.service` daemon.

Read the man at [`systemd-networkd`](https://manpages.debian.org/stretch/systemd/systemd-networkd.8.en.html).

## dhclient
Although not a daemon, [`dhclient`](https://manpages.debian.org/stretch/isc-dhcp-client/dhclient.8.en.html) from [`isc-dhcp-client`](https://packages.debian.org/stretch/isc-dhcp-client) is nonetheless a very important package and often required on desktop distributions as you often need to obtain a IPv4 from a DHCP server.

Hopefully, as IPv6 (which uses [SLAAC](https://en.wikipedia.org/wiki/IPv6_address#Stateless_address_autoconfiguration)) is slowly being adopted, this will probably change in a near or distant future.