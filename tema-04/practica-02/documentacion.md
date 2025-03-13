# Práctica 02: Instalación del Laboratorio con KVM/QEMU
## ✅ 1️⃣ Configuración de la Red en KVM/QEMU
### 📌 Objetivo:
Crear una red NAT con direccionamiento 10.0.2.0/24 para que Kali y Windows 7 puedan comunicarse entre sí y con la máquina anfitriona.

### Pasos:
Verificar que KVM/QEMU está instalado y habilitado:

```bash
sudo apt update
sudo apt install -y qemu-kvm libvirt-daemon-system virt-manager bridge-utils
sudo systemctl enable --now libvirtd
```
Verifica que KVM está activado:

```bash
sudo kvm-ok
```
Crear una red virtual NAT en KVM/QEMU:

Abre Virt-Manager:
```bash
virt-manager
```
En la pestaña Editar > Detalles de la conexión, selecciona Redes Virtuales.
Clic en Agregar y configura lo siguiente:
- Nombre: Red-NAT
- Modo: NAT
- Dirección de red: 10.0.2.0/24
- Habilitar DHCP: (Opcional, pero recomendable)
- Habilitar reenvío de tráfico IPv4: Sí

Guarda y activa la red.
## ✅ 2️⃣ Máquinas Virtuales Necesarias
📌 Máquina de Ataque: Kali Linux
Descargar la ISO de Kali Linux:

```bash
wget -O kali.iso https://cdimage.kali.org/kali-last-release/kali-linux-2024.1-installer-amd64.iso
```
Crear la máquina virtual con KVM/QEMU:

```bash
virt-install --name KaliLinux \
    --ram 4096 \
    --vcpus 2 \
    --disk path=/var/lib/libvirt/images/kali.qcow2,size=30 \
    --os-variant debian11 \
    --cdrom kali.iso \
    --network network=Red-NAT,model=virtio \
    --graphics spice
```
Instalar Kali Linux dentro de la VM y seguir los pasos de instalación.

### 📌 Máquina Víctima: Windows 7 SP1
Descargar Windows 7 SP1 (ISO):
Puedes obtener una ISO desde Archive.org.

Convertir la ISO en un disco instalable:

```bash
qemu-img create -f qcow2 /var/lib/libvirt/images/windows7.qcow2 20G
```
## ✅ 3️⃣ Creación de la Máquina Virtual Windows 7 en KVM/QEMU
Crear e instalar la máquina virtual:

```bash
virt-install --name Win7SP1 \
    --ram 2048 \
    --vcpus 2 \
    --disk path=/var/lib/libvirt/images/windows7.qcow2,format=qcow2 \
    --os-variant win7 \
    --cdrom windows7.iso \
    --network network=Red-NAT,model=virtio \
    --graphics spice
```
Instalar Windows 7 en la VM.

Instalar los Drivers VirtIO (para que funcione la red correctamente):

Descarga el ISO de VirtIO:
```bash
wget -O virtio-win.iso https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso
```
Adjunta el virtio-win.iso a la VM en Virt-Manager y usa los drivers durante la instalación.
## ✅ 4️⃣ Deshabilitar el Firewall en Windows 7
### 📌 Objetivo: Exponer el puerto TCP 445 para pruebas de post-explotación.
### Pasos:
Abre Panel de Control > Firewall de Windows.
Haz clic en Activar o desactivar Firewall de Windows.
Desactiva el firewall en Red Privada y Pública.
Verifica con:
```bash
netsh advfirewall set allprofiles state off
```
## ✅ 5️⃣ Validar la conectividad entre Kali y Windows 7
Desde Kali Linux, verifica la comunicación con Windows 7:

```bash
ping 10.0.2.X
```
Desde Windows 7, verifica con:

```bash
ping 10.0.2.X
```
Si todo está correcto, ya tienes un laboratorio funcional en KVM/QEMU. 🚀

