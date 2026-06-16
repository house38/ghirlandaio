# Menginstall OS

## Menghubungkan ke jaringan wifi
```
iwctl
```
```
station wlan0 get-network
``` 
station wlan0 connect "(nama wifi)"
```
```
exit
```
## Memeriksa partisi
```
lsblk
```
```
cfdiks /dev/partisi [sda/nvme0n1p]
```
```
boot = 3G [EFI system}
root = 95G [Linux filesystem]
```
```
lsblk lagi 
