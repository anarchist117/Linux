# iPXE
## 1. Select Boot Type
| Boot Type | Description | Download |
| --- | --- | --- |
| ISO | Pre-built binaries | https://ipxe.org/download |
| TFTP | Chainloading iPXE | https://ipxe.org/howto/chainloading |
| ROM | Burning iPXE into ROM | https://ipxe.org/howto/romburning |

## 2. Configure DHCP Server
[Microsoft DHCP server](https://ipxe.org/howto/msdhcp)

[ISC dhcpd](https://ipxe.org/howto/dhcpd)

or
```
Boot iPXE
Ctrl-B
dhcp
chain http://boot.ipxe.org/demo/boot.php
```







# Documentation
https://ipxe.org/
