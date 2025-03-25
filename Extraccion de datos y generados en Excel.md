

Aquí tienes la explicación detallada de tu código, **sección por sección**, para que entiendas qué hace cada parte. 🚀

---

## 🔹 **1. Verificar la Versión de Python**

```python
!python3 --version
```

✅ **Explicación:**

- El comando `!python3 --version` muestra la versión de Python instalada en el entorno.
- En **Google Colab**, suele ser **Python 3.10 o superior**.

---

## 🔹 **2. Verificar la Versión de Pandas**

```python
import pandas as pd
pd.__version__
```

✅ **Explicación:**

- Se importa la librería `pandas`, utilizada para trabajar con datos tabulares.
- `pd.__version__` muestra la versión instalada de `pandas`.
- **Ejemplo de salida:** `"1.5.3"`

---

## 🔹 **3. Instalar la Librería `PyPDF2`**

```python
!pip install PyPDF2
```

✅ **Explicación:**

- `PyPDF2` es una librería que permite **leer y manipular archivos PDF**.
- Sin embargo, en este código **no se usa** `PyPDF2`, sino `PyMuPDF` (`fitz`).
- Si quieres trabajar con `PyMuPDF`, usa:
    
    ```python
    !pip install pymupdf
    ```
    

---

## 🔹 **4. Subir Archivos desde la Computadora a Google Colab**

```python
from google.colab import files
uploaded = files.upload()
```

✅ **Explicación:**

- `files.upload()` abre una ventana para **subir archivos manualmente** desde tu PC a Google Colab.
- Se puede usar para **subir los PDFs** que se van a analizar.

---

## 🔹 **5. Verificar que los Archivos se Subieron Correctamente**

```python
import os
print(os.listdir())  # Muestra todos los archivos en el entorno
```

✅ **Explicación:**

- `os.listdir()` lista todos los archivos en el entorno de Colab.
- Permite verificar si los PDFs se subieron correctamente.

📌 **Ejemplo de salida esperada:**

```
['documento_ley_comercio.pdf', 'documento_ley_datos.pdf', ...]
```

---

## 🔹 **6. Leer y Mostrar el Contenido de los PDFs**

```python
import fitz  # PyMuPDF

# Lista de PDFs
pdf_files = [
    "documento_ley_comercio.pdf",
    "documento_ley_datos.pdf",
    "documento_ley_propiedad.pdf",
    "documento_ley_seguridad.pdf",
    "documento_ley_transparencia.pdf"
]

# Leer y mostrar el contenido de cada PDF
for pdf_document in pdf_files:
    print(f"\n--- Contenido de {pdf_document} ---\n")
    
    doc = fitz.open(pdf_document)

    for page_num in range(len(doc)):
        text = doc[page_num].get_text()
        print(text)  # Muestra todo el texto del PDF para analizarlo

    doc.close()
```

✅ **Explicación:**

- `fitz.open(pdf_document)` abre cada PDF.
- `doc[page_num].get_text()` extrae el texto de cada página.
- Muestra en consola el contenido de los PDFs **para verificar** que los datos están bien estructurados.

📌 **Si el texto extraído no es correcto, debes revisar la estructura del PDF.**

---

## 🔹 **7. Extraer Datos de los PDFs y Guardarlos en un DataFrame**

```python
import fitz  # PyMuPDF
import pandas as pd

# Lista de PDFs
pdf_files = [
    "documento_ley_comercio.pdf",
    "documento_ley_datos.pdf",
    "documento_ley_propiedad.pdf",
    "documento_ley_seguridad.pdf",
    "documento_ley_transparencia.pdf"
]

# Lista para almacenar datos
data = []

# Extraer datos
for pdf_document in pdf_files:
    doc = fitz.open(pdf_document)

    for page_num in range(len(doc)):
        text = doc[page_num].get_text("text").split("\n")  # Obtener texto línea por línea
        
        # Buscar la posición del primer dato (evitar encabezados)
        start_index = None
        for i, line in enumerate(text):
            if line.strip().isdigit():  # Si una línea es un número, asumimos que es un ID
                start_index = i
                break
        
        if start_index is not None:
            # Extraer datos de la tabla
            for i in range(start_index, len(text), 4):
                try:
                    row = [text[i], text[i+1], text[i+2], text[i+3]]
                    data.append(row)
                except IndexError:
                    continue

    doc.close()

# Crear DataFrame
df = pd.DataFrame(data, columns=["ID", "Nombre", "Fecha", "Tipo de Ley"])
```

✅ **Explicación:**

- Extrae los datos del PDF y los guarda en la lista `data`.
- Se busca la **primera fila de datos reales** (saltando encabezados).
- Los datos se agrupan de 4 en 4 (`ID, Nombre, Fecha, Tipo de Ley`).
- `pd.DataFrame(data, columns=...)` crea un DataFrame con las columnas estructuradas.

---

## 🔹 **8. Limpiar y Formatear los Datos**

```python
# Verificar si hay datos en el DataFrame
if df.empty:
    print(" No se extrajeron datos. Revisa la estructura del PDF.")
else:
    # Convertir ID a número
    df["ID"] = pd.to_numeric(df["ID"], errors="coerce").astype("Int64")

    # Convertir la columna "Fecha" a formato datetime
    df["Fecha"] = pd.to_datetime(df["Fecha"], format="%Y-%m-%d", errors="coerce")

    # Reorganizar en formato Día-Mes-Año (DD-MM-YYYY)
    df["Fecha"] = df["Fecha"].dt.strftime("%d-%m-%Y")

    # Eliminar filas con valores inválidos y reiniciar índices
    df = df.dropna().reset_index(drop=True)

# Mostrar el DataFrame con la fecha en el nuevo formato
print(df)
```

✅ **Explicación:**

- **Verifica si el DataFrame está vacío** (`df.empty`).
- **Convierte `ID` a número** (`pd.to_numeric()`).
- **Convierte `Fecha` a formato Día-Mes-Año (`DD-MM-YYYY`)** con `.dt.strftime("%d-%m-%Y")`.
- **Elimina datos inválidos** (`df.dropna()`).

---

## 🔹 **9. Guardar los Datos en un Archivo Excel**

```python
excel_filename = "datos_extraidos.xlsx"  # Guardar en el directorio actual
df.to_excel(excel_filename, index=False)
print(f" Archivo guardado como {excel_filename}")
```

✅ **Explicación:**

- Guarda el DataFrame como un archivo **Excel** con `df.to_excel()`.
- **`index=False`** evita que pandas agregue una columna extra con el índice.

---

## 🔹 **10. Descargar el Archivo Excel**

```python
from google.colab import files
files.download("datos_extraidos.xlsx")  # Descarga desde el directorio actual
```

✅ **Explicación:**

- `files.download()` permite descargar el archivo desde Google Colab.
- Se debe ejecutar **después de generar el Excel**.

---

##  **Resumen**

✅ **Se suben los PDFs a Colab.**  
✅ **Se extrae y organiza el texto en un DataFrame.**  
✅ **Se formatea la fecha en `DD-MM-YYYY`.**  
✅ **Se exporta a Excel y se descarga.**

Con esto tienes una **extracción completa de datos desde PDFs a un formato estructurado**.  
Si necesitas más explicaciones o mejoras, dime. 