# Práctica 01: Proceso de Cracking de Contraseñas con Hashcat
## 1. Preparación del Diccionario - Modificar rockyou.txt
Vamos a añadir la palabra `hashcat` a `rockyou.txt`.
1. En Kali, `rockyou.txt` ya viene instalado
   ![1741277380591](image/documentacion/1741277380591.png)
2. Siendo superusuario, escribimos el siguiente comando
   ![1741277697337](image/documentacion/1741277697337.png)

## 2. Descifrado de Hashes con Hashcat
Hashcat es un potente descifrador de contraseñas que admite diferentes tipos de hash.
### 1. Descifrar Hash MD5
El hash a descifrar es el siguiente:
```sh
8743b52063cd84097a65d1633f5c74f5
```
1. Escribimos el siguiente comando:
![1741277952861](image/documentacion/1741277952861.png)
2. Tras esperar un poco, se nos habrá generado el archivo con la contraseña crackeada:
![1741278005200](image/documentacion/1741278005200.png)

### 2. Descifrar Hash NTLM
![1741278098123](image/documentacion/1741278098123.png)
![1741278166169](image/documentacion/1741278166169.png)
![1741278203239](image/documentacion/1741278203239.png)

### 3. Descifrar Hash NETNTLMv2
![1741278271193](image/documentacion/1741278271193.png)
![1741278306858](image/documentacion/1741278306858.png)
![1741278335322](image/documentacion/1741278335322.png)