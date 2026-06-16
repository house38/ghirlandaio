# Menginstall OS

## Menghubungkan ke jaringan wifi
```
iwctl
device list
```
Cek driver wifi setiap laptop
```
station wlan0 get-network
```
Melihat jaringan yang tersedia
```
station wlan0 scaan
```
Memindaai jaringan yang ada
```
station wlan0 connect "(nama wifi)"
exit
```
## Memeriksa partisi
```
lsblk
```
```
cfdiks /dev/partisi [sda/nvme0n1p1]
```
```
boot = 3G [EFI system}
root = 95G [Linux filesystem]
```
```
lsblk lagi
```
## Format LUKS
```
cryptsetup luksFormat /dev/[partisi root]
```
```
masukkan kata sandi
```
```
cryptsetup luksOpen /dev/[partisi root] [nama device]
```
```

