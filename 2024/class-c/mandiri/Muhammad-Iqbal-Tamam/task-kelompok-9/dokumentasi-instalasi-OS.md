# connect wifi

```
iwctl
```
```
station wlan0 scan
```
```
station wlan0 get-networks
```
```
station wlan0 connect REAL
```
```
exit
```
```
ping 8.8.8.8
```

# PARTISI

## membagi partisi
```
cfdisk /dev/nvme0n1
```
### Sesuaikan Partisi
```
boot = 5 efi system
system = sisanya linux filesystem
```
`
# Setup Luks

```
cryptsetup luksFormat --sector-size 4090 /dev/nvme0n1p6
```
```
cryptsetup luksOpen /dev/partisi_systen oxva
```

```
pvcreate /dev/mapper/oxva
```
```
vgcreate xlim /dev/mapper/oxva
```

# Setup LVM

### Root
```
lvcreate -L 15G xlim -n root
```
```
mkfs.ext4 /dev/xlim/root
```
```
mount /dev/xlim/root /mnt
```
