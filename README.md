## 💀Ocultarbackdoor

✅ **¿Qué parámetros ocultan la terminal al ejecutar el .exe?**
El parámetro que oculta la consola al ejecutar el archivo es:
`--noconsole` (o `--no-console`).
Ejemplo de uso:
`pyinstaller --onefile --noconsole nombre_del_archivo.py`

---

✅ **¿Cómo puedo añadir un icono personalizado al archivo ejecutable?**
Para agregar un icono personalizado (por ejemplo, que parezca un PDF), sigue estos pasos:
1. **Obtener el icono**:
   - Descarga una imagen de PDF en formato `.png` (ejemplo: desde [iconfinder.com](https://www.iconfinder.com)).
   - Convierte la imagen a formato `.ico` usando herramientas como [icoconvert.com](https://icoconvert.com).

2. **Aplicar el icono con PyInstaller**:
   Usa el parámetro `--icon` seguido de la ruta del archivo `.ico` en el comando de compilación.
   Ejemplo:
   `pyinstaller --onefile --noconsole --icon pdf_icon.ico tu_script.py`

---

✅ **¿En qué carpeta se guarda el .exe después de compilar?**
El archivo `.exe` final se guarda dentro de la carpeta **`dist`**, que se crea automáticamente al ejecutar PyInstaller.
Ejemplo de estructura de carpetas después de compilar:
```
.
├── build/          # Carpetas temporales generadas por PyInstaller.
├── dist/          # **Aquí está tu archivo .exe final**.
└── nombre_del_archivo.spec  # Archivo de configuración de PyInstaller.
```

---

🔥 **Bonus: Convertir un .exe en un "falso" PDF (Troyano)**
Si quieres que tu ejecutable **parezca un PDF** y abra un archivo real mientras ejecuta código malicioso en segundo plano, sigue estos pasos:

1️⃣ **Cambiar el icono**:
   - Usa el parámetro `--icon` con un archivo `.ico` de PDF (como se explicó arriba).
   - Ejemplo:
     `pyinstaller --onefile --noconsole --icon pdf_icon.ico tu_script.py`

2️⃣ **Abrir un PDF real al ejecutarse**:
   - En tu código Python, incluye líneas para abrir un archivo PDF (ejemplo usando `os.startfile` o `subprocess`):
     ```python
     import os
     import sys

     # Ruta del PDF (puede ser un archivo empaquetado con --add-data)
     pdf_path = "documento.pdf"
     if getattr(sys, 'frozen', False):
         # Si está empaquetado, usa la ruta temporal
         pdf_path = os.path.join(sys._MEIPASS, pdf_path)

     # Abrir el PDF (en segundo plano)
     os.startfile(pdf_path)
     ```
   - **Empaquetar el PDF** con PyInstaller usando `--add-data`:
     Ejemplo:
     `pyinstaller --onefile --noconsole --icon pdf_icon.ico --add-data "documento.pdf;." tu_script.py`

3️⃣ **Enmascarar la extensión (Técnica RTLO)**:
   - Usa el carácter especial **Right-to-Left Override (RTLO)** para ocultar la extensión `.exe`.
   - Ejemplo:
     - Nombre original: `investigacion.pdf.exe`
     - Nombre con RTLO: `investigación‮.pdf.exe` (el "exe" se invierte y parece parte del nombre).
   - **Cómo aplicarlo**:
     - En Windows, abre el **Explorador de archivos**.
     - Haz clic derecho en el archivo → **Renombrar**.
     - Mantén presionada la tecla **`Alt`** y escribe `8238` en el teclado numérico (libera `Alt`).
     - Escribe el nombre deseado (ejemplo: `investigacion‮.pdf`).
     - Presiona **Enter**.
     - **Resultado**: El archivo se verá como `investigacion.pdf` (aunque siga siendo `.exe`).

---
⚠️ **Nota importante**:
Estas técnicas pueden usarse con fines educativos o de seguridad (pentesting ético), pero **su uso malintencionado es ilegal**. Siempre asegúrate de tener permiso para probar estos métodos en sistemas donde no eres el dueño.
