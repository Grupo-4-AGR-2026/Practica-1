# Practica-1

Diseño de un centro de datos bare metal — Arquitectura, dimensionamiento, direccionamiento, routing, seguridad y costes.

---

## Compilación de la Memoria (`mem.tex`)

El documento principal del proyecto está modularizado en LaTeX (`mem.tex`) e incluye
las secciones ubicadas en el directorio `sections/`.

> [!WARNING]
> Asegúrese de cerrar `mem.pdf` (o el visor de PDF en uso) antes de compilar el documento.
En sistemas Windows, los visores de PDF bloquean el archivo, impidiendo que el compilador sobrescriba el resultado
y provocando errores de compilación (`Permission denied` o `I can't write on file`).

### Requisitos previos

Es necesario disponer de una distribución de LaTeX instalada en el sistema:

- **Windows / Linux / macOS**: [TeX Live](https://www.tug.org/texlive/) o [MiKTeX](https://miktex.org/).
- Paquetes principales requeridos: `inputenc`, `fontenc`, `babel`, `geometry`, `amsmath`, `graphicx`, `listings`,
  `hyperref`, `tabularx`, `booktabs`, `caption`, `subcaption`.

---

### Instrucciones de compilación

#### Opción 1: Compilación manual con `pdflatex`

Si se utiliza directamente el compilador base `pdflatex`, se deben ejecutar dos pasadas consecutivas para generar y
actualizar correctamente la tabla de contenidos y las referencias cruzadas:

```bash
pdflatex -output-directory=out mem.tex
pdflatex -output-directory=out mem.tex
```

O sin redirigir la salida a la carpeta `out/`:

```bash
pdflatex mem.tex
pdflatex mem.tex
```

#### Opción 2: Automatizada con `latexmk`

`latexmk` gestiona automáticamente las pasadas necesarias para resolver enlaces, índice, tablas y figuras:

```bash
latexmk -pdf mem.tex
```

Para compilar y enviar los archivos auxiliares a un directorio de salida (e.g., `out/`):

```bash
latexmk -pdf -outdir=out mem.tex
```

---

### Limpieza de archivos temporales

Para eliminar los archivos auxiliares generados durante la compilación (`.aux`, `.log`, `.toc`, `.out`, `.lof`, `.lot`,
etc.):

- **Con `latexmk`**:
  ```bash
  latexmk -c mem.tex
  ```
  *(O `latexmk -C mem.tex` para eliminar también el PDF resultante).*

- **En PowerShell (Windows)**:
  ```powershell
  Remove-Item -Path *.aux, *.log, *.toc, *.out, *.lof, *.lot, *.fls, *.fdb_latexmk -ErrorAction SilentlyContinue
  ```

- **En Bash (Linux/macOS)**:
  ```bash
  rm -f *.aux *.log *.toc *.out *.lof *.lot *.fls *.fdb_latexmk
  ```

[//]: # (Author = javierdesant, morteega, dagalle, jorge)
