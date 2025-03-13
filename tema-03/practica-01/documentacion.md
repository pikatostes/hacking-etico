# Práctica 01 - Fase de Reconocimiento¶
## Ejercicio 1 - Buscar todos los archivos PDF del sitio github.com.
El siguiente comando depura los resultados en Google para que aparezcan únicamente archivos `.pdf` alojados en `https://github.com`.
```zsh
site:github.com filetype:pdf
```

## Ejercicio 2 - Buscar cualquier URL que contenga la cadena intranet/login.php.
Con el siguiente comando buscamos URLs que contengan la cadena exacta indicada. Eficaz para encontrar rutas concretas en aplicaciones web.
```zsh
inurl:"intranet/login.php"
```

## Ejercicio 3 - Buscar un listado de directorios con la carpeta uploads expuesta.
El siguiente comando busca páginas de índice (listados de directorios) a la vez que filtra aquellas con el subdirectorio `/uploads`.
```zsh
intitle:"index of" inurl:"/uploads"
```

## Ejercicio 4 - Buscar documentos Word (.docx) que contengan información sensible.
Este comando busca documentos del tipo indicado con la palabra clave "confidential". Puede localizar documentos mal protegidos.
filetype:docx "confidential"
