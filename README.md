On my laptop, I restrict all outgoing connections on port 53. All unencrypted DNS traffic is blocked. This creates issues when I am using public wifi, where I need to login to some captive portal.

This script performs the following actions automatically:

1. Discovers the DNS resolver offered by the public wifi network (via dhcp),
2. Temporarily whitelists the (unencrypted, port53 on udp) DNS resolver with ipfw,
3. Discovers the hostname of the captive portal,
4. Inserts a forward-zone rule into unbound, allowing unbound to resolve the captive portal address using the DNS resolver offered by the public wifi.

The only thing the script doesn't do is remove the whitelisted DNS resolver from ipfw. But if your system is configured correctly, the resolver shouldn't be used: only by unbound for resolving very specific addresses (required by the captive portal).

To be run as root, as `./captive-unbind wifibox0` where `wifibox0` is the wifi ssid / dhclient name.

A little bit more information about this script can be found [on this post](https://joshua.hu/captive-portal-automatic-unbound-resolve-forward-zone-blocked-dns-traffic).
