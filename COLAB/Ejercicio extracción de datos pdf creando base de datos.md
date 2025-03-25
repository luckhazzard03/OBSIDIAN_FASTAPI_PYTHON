
Para convertir este proceso en una **base de datos relacional**, puedes usar **SQLite3** con SQLAlchemy, lo que permitirá almacenar los datos en tablas estructuradas y consultarlas fácilmente.

---

##  **Pasos para Crear una Base de Datos Relacional en SQLite3**

###  **1. Instalar SQLAlchemy (si no lo tienes)**

```python
!pip install sqlalchemy
```

###  **2. Definir el Modelo de la Base de Datos**

Vamos a usar **SQLAlchemy** para definir una base de datos relacional con una tabla **"leyes"** que almacene los datos extraídos.

```python
from sqlalchemy import create_engine, Column, Integer, String, Date
from sqlalchemy.orm import declarative_base, sessionmaker

  

# Crear la conexión a SQLite

engine = create_engine("sqlite:///leyes.db")
Base = declarative_base()

  

# Definir el modelo de datos

class Ley(Base):
    __tablename__ = "leyes"

  

    id = Column(Integer, primary_key=True, autoincrement=True)  # SQLite generará el ID automáticamente

    nombre = Column(String, nullable=False)
    fecha = Column(Date, nullable=False)
    tipo_ley = Column(String, nullable=False)

  

# Crear la base de datos y la tabla

Base.metadata.create_all(engine)

  

# Crear una sesión para interactuar con la base de datos

Session = sessionmaker(bind=engine)  # Corregido sessionmaker
session = Session()
  

print("✅ Base de datos y tabla creadas correctamente.")

```

📌 **Explicación:**  
✅ Se define una tabla `leyes` con **ID, Nombre, Fecha y Tipo de Ley**.  
✅ Se usa `create_engine("sqlite:///leyes.db")` para conectar a **SQLite**.  
✅ Se crea la tabla en la base de datos con `Base.metadata.create_all(engine)`.

---

###  **3. Extraer los Datos de los PDFs y Guardarlos en la Base de Datos**

Este código extrae los datos como antes, pero en vez de guardarlos en un `DataFrame`, **los almacena en SQLite**.

```python
import fitz  # PyMuPDF

from datetime import datetime

  

# Lista de PDFs

pdf_files = [
    "documento_ley_comercio.pdf",
    "documento_ley_datos.pdf",
    "documento_ley_propiedad.pdf",
    "documento_ley_seguridad.pdf",
    "documento_ley_transparencia.pdf"

]

  

# Extraer datos y guardarlos en la BD

for pdf_document in pdf_files:
    doc = fitz.open(pdf_document)  

    for page_num in range(len(doc)):
        text = doc[page_num].get_text("text").split("\n")  # Obtener texto línea por línea
        
        # Buscar la posición del primer dato (evitar encabezados)

        start_index = None
        for i, line in enumerate(text):
            if line.strip().isdigit():  # Si una línea es un número, asumimos que es un ID
                start_index = i
                break

        if start_index is not None:
            for i in range(start_index, len(text), 4):
                try:
                    # Extraer datos
                    nombre = text[i+1].strip()
                    fecha = datetime.strptime(text[i+2].strip(), "%Y-%m-%d").date()
                    tipo_ley = text[i+3].strip()

  

                    # Insertar en la base de datos SIN ID (SQLite lo genera automáticamente)

                    nueva_ley = Ley(nombre=nombre, fecha=fecha, tipo_ley=tipo_ley)
                    session.add(nueva_ley)
                except (IndexError, ValueError):
                    continue  # Evita errores por datos incompletos

  

    doc.close()
  

# Guardar los cambios en la BD
session.commit()

print("✅ Datos guardados en SQLite correctamente.")
```

📌 **Explicación:**  
✅ Extrae los datos del PDF como antes.  
✅ Convierte **las fechas a formato `DATE` en SQLite**.  
✅ **Guarda los datos en SQLite** en la tabla `leyes`.

---

###  **4. Consultar los Datos desde la Base de Datos**

Una vez guardados los datos en **SQLite**, podemos consultarlos así:

```python
# Consultar datos de la BD
leyes = session.query(Ley).all()

# Convertir a DataFrame para visualización
df = pd.DataFrame([(l.id, l.nombre, l.fecha.strftime("%d-%m-%Y"), l.tipo_ley) for l in leyes], 
                  columns=["ID", "Nombre", "Fecha", "Tipo de Ley"])

print(df)
```

📌 **Salida esperada en consola:**

```
   ID           Nombre        Fecha                   Tipo de Ley
0   1      Juan Pérez   21-03-2024   Ley de Protección de Datos
1   2    María López   14-06-2023   Ley de Protección de Datos
2   3    Carlos Díaz   30-08-2022   Ley de Protección de Datos
3   4     Ana Gómez   25-02-2021   Ley de Protección de Datos
4   5  Pedro Ramírez   18-09-2020   Ley de Protección de Datos
```

---

### 🔹 **5. Exportar la Base de Datos a Excel**

Si quieres exportar los datos desde SQLite a Excel:

```python
# Consultar datos y exportar a Excel
df.to_excel("leyes.xlsx", index=False)

# Descargar el archivo en Google Colab
from google.colab import files
files.download("leyes.xlsx")
```

---

##  **Resumen**

1️⃣ **Creamos una base de datos SQLite con SQLAlchemy.**  
2️⃣ **Extraemos los datos de los PDFs y los almacenamos en una tabla relacional.**  
3️⃣ **Consultamos los datos desde SQLite y los convertimos en un DataFrame.**  
4️⃣ **Exportamos los datos a Excel para su análisis.**

Con esta solución tienes una **base de datos relacional completa** en SQLite.  
Si necesitas adaptar el modelo a MySQL o PostgreSQL, dime y te ayudo. 