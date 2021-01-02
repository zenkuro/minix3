# Minix3

This repository contains guides and automation tools for Minix development.


## Install centos

```console
qemu-kvm  -net user -net nic -m 2G -cdrom CentOS-7-x86\_64-Minimal-2009.iso -hda ./centos.img -boot d -blockdev driver=raw,node-name=disk,file.driver=file,file.filename=centos.img
```
Finish installation by enabling network

```console
qemu-kvm  -net user -net nic -m 2G -hda ./centos.img -boot d -blockdev driver=raw,node-name=disk,file.driver=file,file.filename=centos.img
```
## Enable internet in centos
On boot: yes

## Start centos iwth port forwarding


One thing that is left is forwarding ssh port from your machine into VM
```console
qemu-kvm  -net user,hostfwd=tcp::2222-:22 -net nic,model=virtio  -m 2G -hda ./centos.img -boot d -blockdev driver=raw,node-name=disk,file.driver=file,file.filename=centos.img
```
Now you should be able to login into CentOS over ssh.

```console
ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no -p 2222 root@localhost
```

Install all necesssary packages
```console
sudo yum install vim git zlib-devel zlib  elfutils-devel bzip2  patch
```

Then you can follow guides:

1. https://wiki.minix3.org/doku.php?id=developersguide:crosscompiling
2. https://wiki.minix3.org/doku.php?id=developersguide:minixonarm

Unfortunatly this guide do not allow to croscompile for i86
