# Práctica 02.- 🛠 Instalación del Laboratorio con KVM/QEMU
Este procedimiento permitirá montar un laboratorio con Kali Linux como máquina de ataque y Metasploitable2 como máquina víctima, utilizando KVM/QEMU y una red NAT para facilitar la comunicación entre ambas.

## 1️⃣ Instalación de KVM/QEMU y virt-manager
En sistemas Debian/Ubuntu, instalar los paquetes necesarios:

```bash
sudo apt update
sudo apt install -y qemu-kvm libvirt-daemon libvirt-daemon-system libvirt-clients bridge-utils virt-manager
```
Habilitar y arrancar el servicio de libvirt:

```bash
sudo systemctl enable libvirtd
sudo systemctl start libvirtd
```
Añadir el usuario al grupo libvirt para evitar problemas de permisos:

```bash
sudo usermod -aG libvirt $USER
```
👉 Cerrar sesión y volver a iniciarla para que los cambios surtan efecto.

## 2️⃣ Creación de la Red NAT (10.0.2.0/24)
### 📌 Método 1: Usando virt-manager (Interfaz gráfica)
1. Abrir virt-manager.
2. Ir a Editar > Detalles de la conexión > Redes virtuales.
3. Crear una nueva red virtual:
   - Nombre: red-nat
   - Dirección: 10.0.2.0/24
   - Habilitar DHCP (opcional).
   - Configurar el modo de red como NAT.

    Guardar y activar la red.
### 📌 Método 2: Usando virsh (Línea de comandos)
Crear un archivo de configuración XML (red-nat.xml):
```xml
<network>
  <name>red-nat</name>
  <forward mode='nat'/>
  <ip address='10.0.2.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='10.0.2.2' end='10.0.2.254'/>
    </dhcp>
  </ip>
</network>
```
Aplicar la configuración:
```bash
virsh net-define red-nat.xml
virsh net-start red-nat
virsh net-autostart red-nat
```
### 3️⃣ Creación de la Máquina Virtual Kali Linux
1. Descargar la ISO de Kali Linux
2. Descargar la última versión de Kali Linux desde el sitio oficial.

3. Crear la máquina virtual en virt-manager
4. Abrir virt-manager y hacer clic en "Crear una nueva máquina virtual".
5. Seleccionar "Instalar desde una imagen ISO" y elegir la ISO de Kali Linux.
6. Configurar:
   - CPU: 2 núcleos (mínimo).
   - RAM: 4 GB (recomendado).
   - Disco: 20 GB en formato qcow2.
   - Configurar la red seleccionando red-nat.
7. Iniciar la instalación de Kali Linux.
### 4️⃣ Creación de la Máquina Virtual Metasploitable2
1. Descargar Metasploitable2
2. Descargar la imagen de Metasploitable2 desde Rapid7.

3. Convertir la imagen VMDK a qcow2
4. Normalmente, Metasploitable2 viene en formato VMDK, que debemos convertir a qcow2:

```bash
qemu-img convert -f vmdk -O qcow2 Metasploitable.vmdk Metasploitable.qcow2
```
5. Crear la máquina virtual en virt-manager
6. Abrir virt-manager y hacer clic en "Crear una nueva máquina virtual".
7. Seleccionar "Importar imagen de disco existente".
8. Elegir Metasploitable.qcow2.
9. Configurar:
   - CPU: 1 núcleo.
   - RAM: 512 MB (mínimo).
   - Disco: Se usará Metasploitable.qcow2.
   - Configurar la red seleccionando red-nat.
10. Finalizar la configuración e iniciar la máquina.

✅ Verificación de Conectividad
Para asegurarnos de que ambas máquinas pueden comunicarse dentro de la red red-nat, ejecutamos en Kali Linux:

```bash
ping 10.0.2.X  # (Reemplazar X con la IP de Metasploitable2)
```
Si la conectividad es exitosa, significa que la red está bien configurada y el laboratorio está listo para pruebas de explotación.