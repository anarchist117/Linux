# 1. Find PCI vendor and device IDs
```
lspci -nn

03:00.0 Ethernet controller [0200]: Broadcom Inc. and subsidiaries NetXtreme BCM5720 Gigabit Ethernet PCIe [14e4:165f]
03:00.1 Ethernet controller [0200]: Broadcom Inc. and subsidiaries NetXtreme BCM5720 Gigabit Ethernet PCIe [14e4:165f]

PCI vendor ID is 14e4
PCI device ID is 165f
```

# 2. Building the ROM image
```
apt install -y gcc binutils make perl syslinux liblzma-dev

git clone https://github.com/ipxe/ipxe.git
cd ipxe/src/

# PCI vendor ID + PCI device ID.rom
make bin/14e4165f.rom
```

# 3. Burning the iPXE ROM
### Download  B57udiag-17.2.03.zip
[NetLink®/NetXtreme® I Desktop/Mobile/Server Diagnostic](https://www.broadcom.com/support/download-search?dk=&pa=&pf=Legacy+Ethernet+Controllers&pg=Legacy+Products&pn=BCM57780&po=)

### Start MS-DOS
```
cd B57udiag

B57udiag.exe -ver
B57udiag.exe -c 0 -pxe 14e4165f.rom
```
