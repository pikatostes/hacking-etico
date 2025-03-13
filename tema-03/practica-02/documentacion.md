# Práctica 02 - Instalación del Laboratorio con KVM/QEMU
## 1. Instalación de paquetes necesarios
- Actualizamos los repositorios e instalamos los siguientes paquetes:
```zsh
sudo apt update
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager
```
De esta manera nos aseguramos de que el sistema tenga todo lo necesario para crear y gestionar máquinas virtuales.

## 2. Verificación del soporte de virtualización
- Comprobamos primero que nuestra CPU soporta virtualización:
```zsh
egrep -c '(vmx|svm)' /proc/cpuinfo
```
Si nos aparece un número mayor a 0, nuestra CPU soporta virtualización.

## 3. Configuración de red
- Creamos un puente de red para que las VMs accedan a la red externa
- Editamos el archivo de configuración de red:
```zsh
sudo nano /etc/netplan/01-netcfg.yaml
```
- Configuramos el puente con el siguiente ejemplo:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
  bridges:
    br0:
      interfaces: [enp0s3]
      dhcp4: yes
```
- Aplicamos la configuración:
```zsh
sudo netplan apply
```
## 4. Creación de una máquina virtual
- Creamos una imagen de disco para la VM:
```zsh
qemu-img create -f qcow2 /var/lib/libvirt/images/mi_vm.qcow2 20G
```
- Iniciamos el asistente de creación de VMs con virt-manager o con el comando:
```zsh
virt-install --name mi_vm --ram 2048 --vcpus 2 --disk path=/var/lib/libvirt/images/mi_vm.qcow2,format=qcow2 --os-type linux --os-variant ubuntu20.04 --network bridge=br0 --graphics spice --cdrom /path/to/ubuntu.iso
```
Exactamente, este comando configura una VM con 2 GB de RAM, 2 CPUs, y un puente de red.

## 5. Prueba del laboratorio¶
- Nos aseguramos de que la VM se haya creado correctamente y que puede acceder a la red externa haciendo un ping:
```zsh
ping google.com
```