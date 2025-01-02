# DHCP Options
```
60 = Client Identifier (set to "PXEClient")
66 = Boot Server Host Name
67 = BootFile NameWhen the initial DHCP offer from the DHCP server contains these boot options, an attempt is made to connect to port 4011 on the DHCP server. This offer fails if the PXE server is on another computer.
```
