# PCI Passthrough Setup

- Install required packages
```sudo apt-get install libvirt-bin bridge-utils virt-manager qemu-kvm ovmf```
- Add kernel parameter to `/etc/default/grub` and apply with `update-grub`  
```GRUB_CMDLINE_LINUX_DEFAULT="intel_iommu=on"```
- Add modules to `/etc/modules`
```
vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd
```
- Blacklist nouveau driver?
```
#/etc/modprobe.d/blacklist-nouveau.conf
blacklist nouveau
```
- Prevent GPU from being snatched up during boot
```
#/etc/modprobe.d/vfio.conf
options vfio-pci ids=10de:1b81,10de:10f0
```
- Apply changes with `sudo update-initramfs -u`
