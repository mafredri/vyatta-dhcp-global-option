# vyatta-dhcp-global-option

This package adds support for configuring global options for dhclient on Ubiquity Security Gateway.

## Improvements

- Write configured `global-option`s to e.g. `/var/run/dhclient_eth0.conf`
- Re-generate dhclient config on configuration changes

## Installation

Download the latest release from [Releases](https://github.com/mafredri/vyatta-dhcp-global-option/releases).

```
curl -o /tmp/dhcp-global-option-0.0.1-1.deb https://github.com/mafredri/vyatta-dhcp-global-option/releases/download/v0.0.1/dhcp-global-option-0.0.1-1.deb
sudo dpkg -i /tmp/dhcp-global-option-0.0.1-1.deb
```

## Example use cases

This package can be used to request custom dhcp option from the dhcp server (e.g. your ISP).

### Enable option-6rd request

```
configure
set interfaces ethernet eth0 dhcp-options global-option "option option-6rd code 212 = { integer 8, integer 8, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, array of ip-address };"
set interfaces ethernet eth0 dhcp-options client-option "request option-6rd;"
commit
save
```
