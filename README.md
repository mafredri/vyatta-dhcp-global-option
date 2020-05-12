# vyatta-dhcp-global-option

This package adds support for configuring global options for dhclient on Ubiquity Security Gateway.

## Example use case

### Enable option-6rd request

```
configure
set interfaces ethernet eth0 dhcp-options global-option "option option-6rd code 212 = { integer 8, integer 8, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, unsigned integer 16, array of ip-address };"
set interfaces ethernet eth0 dhcp-options client-option "request option-6rd;"
commit
save
```
