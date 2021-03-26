# Minix3

This repository contains guides and automation tools for Minix development.


## Install centos

During instalation set up additional user. Not to mention that you have to remember passwords tha tyou have granted to root and this new user.
Also make your user administrator, so he will be able to use `sudo`.
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


One thing that is left is forwarding port from your machine into VM.
This should simplify your interraction with new environment.
```console
qemu-kvm  -net user,hostfwd=tcp::2222-:22 -net nic,model=virtio  -m 2G -hda ./centos.img -boot d -blockdev driver=raw,node-name=disk,file.driver=file,file.filename=centos.img
```
Now you should be able to login into CentOS over ssh.
```console
ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no -p 2222 root@localhost
```

For security purpouses it would be wise to use public key authentication. 

```console
ssh-keygen -N ''
vim ~/.ssh/authorized_keys
```
Write to file public pair of public key.
By default it should be located in "~/.ssh/<some-key>.pub" on your host system.

Close file and set privilages for authorized keys file.
```console
chmod 700 ~/.ssh/authorized_keys
```
All previous commands was related to CentOS virtual machine.

Now you can ssh into new machine by doing:
```console
ssh -i ~/.ssh/<some-key> -p 2222 <user>@localhost
```
Once you are in lets disable passord authentication for security purpouses
```console
vim /etc/ssh/sshd_config

PasswordAuthentication no
ChallengeResponseAuthentication yes
```

Enable EPEL(needed for x86)
```console
sudo yum install epel-release
sudo yum groupinstall "Development Tools"
```

Update machine by, and restart to make sure every configuration will take effect
```console
sudo yum update
sudo reboot
```

Install all necesssary packages
```console
sudo yum install vim git zlib-devel zlib  elfutils-devel bzip2  patch
```

Then you can follow guides:

1. https://wiki.minix3.org/doku.php?id=developersguide:crosscompiling
2. https://wiki.minix3.org/doku.php?id=developersguide:minixonarm
