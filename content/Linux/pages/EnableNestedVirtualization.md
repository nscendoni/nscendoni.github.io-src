Title: Enable nested virtualization on intel processors
Category: Linux
Date: 2012-12-01 10:02

## Add to the kernel parameters
```
vi /etc/default/grub
...
kvm-intel.nested=1
...
```
## Update grub on fedora
```
grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
```
Reboot and check if it is enabled:
```
cat /sys/module/kvm_intel/parameters/nested
```
