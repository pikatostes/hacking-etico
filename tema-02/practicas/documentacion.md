# 🔍 Análisis y Mejoras en el Diseño de Redes Wi-Fi
## 1️⃣ Red de Invitados (OPEN Wi-Fi)
### 📌 Problemas de seguridad:

1. **Sin cifrado**: Cualquier usuario conectado o en las cercanías puede interceptar el tráfico con herramientas como Wireshark.
2. **Acceso de empleados**: Si los empleados utilizan esta red, sus dispositivos pueden ser vulnerables a ataques MITM o robo de credenciales.
3. **Falta de segmentación**: Si la red de invitados no está correctamente aislada, podría representar un punto de entrada a la infraestructura corporativa.

### 🎯 Posibles ataques:

1. **Ataques MITM (Man-in-the-Middle)**: Un atacante puede interceptar el tráfico y capturar credenciales.
2. **Ataques de phishing y Rogue AP**: Un atacante podría configurar un AP falso con el mismo SSID para engañar a los usuarios y robar datos.
3. **Explotación de dispositivos conectados**: Un atacante podría explotar vulnerabilidades en dispositivos de invitados.

### ✅ Mejoras recomendadas:

1. Implementar WPA2/WPA3-PSK en lugar de una red abierta.
Segmentar la red para que los invitados no puedan acceder a recursos internos.
2. Habilitar un portal cautivo con autenticación temporal para visitantes.
3. Activar restricciones de ancho de banda para evitar abusos de la red.

## 2️⃣ Red de Dispositivos Móviles (BYOD con WPA2-PSK)
### 📌 Problemas de seguridad:

1. **Uso de una clave compartida (PSK)**: Todos los dispositivos utilizan la misma contraseña, lo que facilita su filtración.
2. **Posible acceso desde fuera de la empresa**: Si los empleados que se han trasladado a la fábrica de al lado siguen conectándose, es posible que la red tenga un alcance mayor al esperado.
3. **Acceso a recursos sensibles**: Los empleados pueden acceder a servidores corporativos con dispositivos personales, lo que representa un riesgo si no están bien protegidos.

### 🎯 Posibles ataques:

1. **Ataques de fuerza bruta a WPA2-PSK**: Si la contraseña es débil, podría ser vulnerada.
2. **Captura de tráfico con KRACK**: Vulnerabilidad que permite desencriptar tráfico WPA2.
3. **Dispositivos comprometidos**: Un empleado con malware en su móvil puede poner en riesgo la red.

### ✅ Mejoras recomendadas:

1. Migrar a WPA2-Enterprise con autenticación individual para cada usuario.
2. Reducir la potencia de emisión del AP para evitar conexiones no deseadas desde fuera del edificio.
Implementar segmentación VLAN para limitar el acceso a servicios corporativos.
3. Utilizar un MDM para gestionar los dispositivos BYOD y asegurar que cumplan políticas de seguridad mínimas.

## 3️⃣ Red Corporativa (WPA2-Enterprise)
### 📌 Problemas de seguridad:

1. **Acceso total a la red interna**: Si un atacante obtiene credenciales, puede acceder a la red como si estuviera conectado por cable.
2. **Falta de MDM implementado**: La empresa planea desplegarlo, pero mientras tanto, los dispositivos pueden no cumplir requisitos de seguridad.
3. **Ataques contra el servidor RADIUS**: Si la autenticación 802.1X no está bien configurada, un atacante podría intentar explotar debilidades en el servidor RADIUS.

### 🎯 Posibles ataques:

1. **Ataques Evil Twin**: Un atacante puede simular el AP corporativo y capturar credenciales.
2. **Ataques de suplantación de identidad**: Si las credenciales de un usuario se filtran, pueden ser usadas para acceder a la red.
3. **Explotación de dispositivos**: Un equipo comprometido podría infectar la red interna.

### ✅ Mejoras recomendadas:

1. Desplegar el MDM lo antes posible para controlar dispositivos conectados.
2. Habilitar certificados en lugar de credenciales para la autenticación 802.1X.
3. Implementar segmentación VLAN para limitar el acceso a sistemas críticos.
4. Monitorear la red en busca de APs maliciosos y ataques contra el servidor RADIUS.

## 📌 Conclusión
Cada red tiene vulnerabilidades específicas, pero aplicando segmentación, autenticación segura y herramientas de monitoreo, se pueden minimizar los riesgos. 🚀