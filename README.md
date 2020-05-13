# vyatta-dhcp-global-option

This package adds support for configuring global options for dhclient on UniFi Security Gateway.

## Improvements

- Write configured `global-option`s to e.g. `/var/run/dhclient_eth0.conf`
- Re-generate dhclient config on configuration changes

## Installation

Download the latest release from [Releases](https://github.com/mafredri/vyatta-dhcp-global-option/releases).

```
curl -sSL -o /tmp/dhcp-global-option-0.0.2-1.deb https://github.com/mafredri/vyatta-dhcp-global-option/releases/download/v0.0.2/dhcp-global-option-0.0.2-1.deb
sudo dpkg -i /tmp/dhcp-global-option-0.0.2-1.deb
```

### Restore after firmare upgrade

The UniFi Security Gateway runs a script (`etc/init.d/ubnt-rcS`) after firmware upgrades, it looks for `.deb` packages in `/config/data/firstboot/install-packages` and if there are any, installs them. We can utilize this folder to make sure the package remains installed.

```
mkdir -p /config/data/firstboot/install-packages
mv /tmp/dhcp-global-option-0.0.2-1.deb /config/data/firstboot/install-packages
```

## Example use cases

This package can be used to request custom dhcp option from the dhcp server (e.g. your ISP).

### Enable option-6rd request

```
configure
set interfaces ethernet eth0 dhcp-options global-option "option option-6rd code 212 = { integer 8, integer 8, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, array of ip-address };"
set interfaces ethernet eth0 dhcp-options client-option "also request option-6rd;"
commit
save
```
