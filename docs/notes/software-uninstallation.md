# 软件卸载

## LibreOffice

```shell
sudo apt purge libreoffice*
sudo rm -rf /usr/lib/libreoffice
sudo rm -rf /etc/libreoffice
```

## VMware Workstation Pro

```shell
sudo vmware-installer -u vmware-workstation
```

## VirtualBox

```shell
sudo sh /opt/VirtualBox/uninstall.sh
```

## QEMU + Virtual Machine Manager

在 Virtual Machine Manager 中停止并删除所有虚拟机。

```shell
sudo apt remove qemu-* virt-manager
sudo apt autoremove
sudo rm -rf /var/lib/libvirt
```