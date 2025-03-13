# Práctica 03.- 🛠 Fase de Escaneo con Nmap en Kali Linux
Se realizarán tres tipos de escaneo:

- Escaneo de red 🔍 (descubrir hosts activos).
- Escaneo de servicios 🔧 (detectar puertos abiertos y servicios en ejecución).
- Escaneo de vulnerabilidades 🚨 (detectar posibles fallos de seguridad).
## 1️⃣ Identificar la IP de la Máquina Víctima
Antes de comenzar los escaneos, necesitamos conocer la IP de la máquina Metasploitable2. Para ello, en Kali Linux ejecuta:

```bash
ip a
```
Y en Metasploitable2, inicia sesión con msfadmin/msfadmin y usa:

```bash
ip a
```
Anota la IP (ejemplo: 10.0.2.15).

## 2️⃣ Escaneo de Red (Descubrir hosts activos)
Si no conocemos la IP exacta de Metasploitable2, podemos descubrir los dispositivos activos en la red:

```bash
nmap -sn 10.0.2.0/24
```
Esto hará un ping sweep sobre toda la red 10.0.2.0/24, mostrando qué máquinas están activas.

## 3️⃣ Escaneo de Servicios (Puertos Abiertos y Servicios)
Una vez identificada la IP de la máquina víctima, realizamos un escaneo de puertos abiertos y servicios en ejecución:

```bash
nmap -sS -sV -O -p- 10.0.2.15
```
Explicación:

- sS → Escaneo TCP SYN (sigiloso).
- sV → Detección de versiones de servicios.
- O → Intento de detección de sistema operativo.
- p- → Escanea todos los puertos (1-65535).
Si queremos un escaneo más rápido enfocándonos en los 1000 puertos más comunes:

```bash
nmap -sS -sV -O 10.0.2.15
```
## 4️⃣ Instalación de Vulscan (Para Escaneo de Vulnerabilidades)
Vulscan es un script para Nmap que permite correlacionar los resultados con bases de datos de vulnerabilidades.

### 1️⃣ Clonar el repositorio de Vulscan:

```bash
cd /usr/share/nmap/scripts/
sudo git clone https://github.com/scipag/vulscan.git
```
### 2️⃣ Actualizar la base de datos de vulnerabilidades:

```bash
cd vulscan
sudo ./update.sh
```
## 5️⃣ Escaneo de Vulnerabilidades con Vulscan
Ahora que tenemos Vulscan instalado, ejecutamos:

```bash
nmap -sS -sV --script vulscan/vulscan.nse 10.0.2.15
```
Si queremos usar una base de datos específica, por ejemplo Exploit-DB:

```bash
nmap -sS -sV --script vulscan/vulscan.nse --script-args vulscan.db=exploitdb.csv 10.0.2.15
```
✅ Interpretación de Resultados
Después de los escaneos:

- Escaneo de red nos dice qué máquinas están activas en la red.
- Escaneo de servicios nos muestra qué puertos están abiertos y qué servicios corren en ellos.
- Escaneo de vulnerabilidades nos ayuda a identificar posibles exploits.