# Como pasar un archivo .ova a .qcow2
Como el formato .ova es simplemente un archivo comprimido, puedes extraer los archivos contenidos usando tar
Extrae el archivo .ova:

```bash
tar -xvf nombre_de_la_maquina.ova
```

Convertir el .vmdk a .qcow2: Utiliza qemu-img para convertir el archivo .vmdk a un formato que GNOME Boxes pueda usar:

```bash
qemu-img convert -O qcow2 nombre_de_la_maquina.vmdk nombre_de_la_maquina.qcow2
```

Importar en GNOME Boxes
