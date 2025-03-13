# Práctica 01.-Fase de reconocimiento
## 🔍 1️⃣ Buscar todos los archivos PDF en GitHub
```plaintext
site:github.com filetype:pdf
```
📌 Explicación:

- `site:github.com` → Filtra solo resultados de GitHub.
- `filetype:pdf` → Busca archivos con la extensión .pdf.
## 🔍 2️⃣ Buscar cualquier URL que contenga la cadena intranet/login.php
```plaintext
inurl:intranet/login.php
```
📌 Explicación:

- `inurl:intranet/login.php` → Busca páginas con "intranet/login.php" en la URL.

## 🔍 3️⃣ Buscar directorios con la carpeta uploads expuesta
```plaintext
intitle:"index of" "uploads"
```
📌 Explicación:

- `intitle:"index of"` → Busca listados de directorios abiertos.
- `"uploads"` → Filtra resultados con la carpeta "uploads".

## 🔍 4️⃣ Buscar documentos Word (.docx) con información sensible
```plaintext
filetype:docx "confidential" OR "password" OR "internal use only"
```
📌 Explicación:

- `filetype:docx` → Busca archivos con extensión .docx.
- `"confidential" OR "password" OR "internal use only"` → Filtra documentos con palabras clave que podrían indicar información sensible.
