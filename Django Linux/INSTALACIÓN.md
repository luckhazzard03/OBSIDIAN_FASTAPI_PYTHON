
## Ubuntu 22.04 LTS


Para instalar la extensión **Remote - WSL** desde **la terminal de VS Code**, sigue estos pasos:

### Pasos para instalar la extensión **Remote - WSL** desde la terminal de VS Code

1. **Abrir la terminal de VS Code**: Si aún no tienes **VS Code** abierto, abre **VS Code** desde el menú de inicio o desde la terminal de Windows ejecutando el comando:
    
    bash
    
    `code`
    
2. **Abrir la terminal de VS Code**: Dentro de **VS Code**, abre la terminal integrada con el siguiente atajo de teclado:
    
    - En Windows: `Ctrl + `` (la tecla justo debajo de **Esc**)
    - O puedes abrir la terminal desde el menú: **Terminal > New Terminal**.
3. **Instalar la extensión Remote - WSL** usando la terminal de **VS Code**:
    
    - En la terminal de **VS Code**, ejecuta el siguiente comando:
        
        bash
        
        ```c
            code --install-extension ms-vscode-remote.remote-wsl
        ```
        
    
    Este comando descargará e instalará la extensión **Remote - WSL** de Microsoft directamente desde la terminal.
    
4. **Verificar la instalación**: Una vez que la extensión esté instalada, puedes verificarlo de dos maneras:
    
    - **Desde la terminal**: Ejecutando el comando `code --list-extensions` para ver todas las extensiones instaladas. Deberías ver `ms-vscode-remote.remote-wsl` en la lista.
    - **Desde la interfaz de VS Code**: Ve a la vista de **Extensiones** (Ctrl + Shift + X) y busca **Remote - WSL**. Debería estar instalada y aparecer allí.

### Usar la extensión después de instalarla

Una vez que la extensión **Remote - WSL** esté instalada, puedes abrir una carpeta o proyecto dentro de **WSL** utilizando el siguiente comando en el terminal de **WSL**:

1. Abre la terminal **WSL** (puedes hacerlo desde el terminal de **Ubuntu** o cualquier distribución que tengas en **WSL**).
2. Navega a la carpeta del proyecto o directorio que quieres abrir en **VS Code**.
3. Usa el siguiente comando para abrir la carpeta directamente en **VS Code** en modo **WSL**:
    
    bash
    
    `code .`
    

Esto abrirá **VS Code** en el entorno **Linux (WSL)** y podrás trabajar directamente con los archivos del sistema de archivos de **WSL**.


### 1. Se ejecuta directamente desde  terminal WSL con el comando "wsl -d Ubuntu-22.04".


```c
 PS C:\Users\Usuario> wsl -d Ubuntu-22.04
 luckhazard@GAMERLORDART:/mnt/c/Users/Usuario$ 
```


## Opción 1: Obtener la última versión oficial

La última versión oficial es la 5.1.6. Lee las [notas de la versión 5.1.6](https://docs.djangoproject.com/en/5.1/releases/5.1.6/) y luego instálala con [pip](https://pip.pypa.io/en/latest/) :

Linux / macOS:

```c
python3 -m pip install Django==5.1.6
```

Windows:

```c
py3 -m pip install Django==5.1.6
```

# 2. Cómo escribir tu primera aplicación Django, parte 1

Aprendamos con el ejemplo.

A lo largo de este tutorial, lo guiaremos a través de la creación de una aplicación de encuesta básica.

Constará de dos partes:

- Un sitio público que permite a las personas ver encuestas y votar en ellas.
    
- Un sitio de administración que le permite agregar, cambiar y eliminar encuestas.
    

Supondremos que ya tienes [instalado Django](https://docs.djangoproject.com/en/5.1/intro/install/) . Puedes saber si está instalado Django y cuál es su versión ejecutando el siguiente comando en un indicador de shell (indicado por el prefijo $):

```c
$ python -m django --version
```

## 3. Creando un proyecto

```c
$ mkdir djangotutorial
```
### Luego, ejecute el siguiente comando para iniciar un nuevo proyecto Django:

Según como lo haya nombrado el proyecto, en este caso lo nombre djangotutorial

```c
$ django-admin startproject mysite djangotutorial
```

Sirve para crear una nueva aplicación dentro de tu proyecto Django llamada **"comentarios"**. 

   ```c
   python3 manage.py startapp comentarios
   ```

### **¿Qué es una aplicación en Django?**

En Django, un **proyecto** puede estar compuesto por varias **aplicaciones**. Cada aplicación es un módulo independiente con funcionalidades específicas. Por ejemplo, si tienes un sitio web, podrías tener aplicaciones como:

- `usuarios` → Para gestionar autenticación y perfiles.
- `productos` → Para manejar una tienda en línea.
- `comentarios` → Para gestionar comentarios en publicaciones.
##### **Estructura creada por `startapp`**

Cuando ejecutas el comando, Django genera una carpeta llamada `comentarios/` con la siguiente estructura:

   ```c
  comentarios/
│── migrations/   # Directorio donde se guardan las migraciones de la base de datos
│── __init__.py   # Indica que es un paquete de Python
│── admin.py      # Configuración para el panel de administración de Django
│── apps.py       # Configuración de la aplicación
│── models.py     # Definición de los modelos de base de datos
│── tests.py      # Pruebas unitarias para la aplicación
│── views.py      # Lógica de la aplicación (vistas)

   ```


### **¿Qué hacer después de crearlo?**

### **¿Qué hacer después de crearlo?**

1️⃣ **Registrar la app en el proyecto**  
Abre el archivo `settings.py` de tu proyecto y agrega la nueva app en `INSTALLED_APPS`:


```c
INSTALLED_APPS = [
    ...
    'comentarios',  # Agregamos la nueva aplicación
]

```


2️⃣ **Definir modelos en `models.py`**  
Aquí defines las tablas que se guardarán en la base de datos. Ejemplo:


```c
from django.db import models

class Comentario(models.Model):
    usuario = models.CharField(max_length=100)
    texto = models.TextField()
    fecha = models.DateTimeField(auto_now_add=True)

```


3️⃣ **Crear y aplicar migraciones**  
Después de definir los modelos, ejecuta:

```c
python3 manage.py makemigrations comentarios
python3 manage.py migrate
```



4️⃣ **Definir rutas en `views.py` y `urls.py`**

- En `views.py`:
    
    ```c
    from django.http import HttpResponse

    def lista_comentarios(request):
        return HttpResponse("Lista de comentarios")

    ```
    
    
    
- En `urls.py` del proyecto:
    
```c
from django.urls import path
from comentarios.views import lista_comentarios

urlpatterns = [
    path('comentarios/', lista_comentarios),
]

```
    
        

Ahora, si visitas `http://127.0.0.1:8000/comentarios/`, verás el mensaje "Lista de comentarios".

🔹 **En resumen:** `startapp` crea la estructura de una aplicación en Django, y luego puedes definir modelos, vistas y rutas para hacerla funcional.



### 4. **Acceder al directorio de inicio en Ubuntu (WSL): cd ~**


```c
luckhazard@GAMERLORDART:/mnt/c/Users/Usuario$ cd ~
luckhazard@GAMERLORDART:~$ ls
djangotutorial
```

### 5. abrir en VScode:

```c
code .
```


### 6. Ejecutar el proyecto con el archivo manage.py:

El comando `python3 manage.py migrate` en Django se utiliza para aplicar y sincronizar las migraciones de la base de datos con el modelo de datos de la aplicación.

Cuando se hacen cambios en los modelos (por ejemplo, agregar un campo a un modelo, crear una nueva tabla, etc.), esos cambios deben reflejarse en la base de datos. Las migraciones son una forma de hacer este seguimiento y aplicar cambios a la base de datos de manera ordenada.

### En detalle, lo que hace este comando es:

4. **Aplicar migraciones pendientes**: Si hay migraciones no aplicadas, `migrate` las ejecutará en la base de datos.
5. **Actualizar la base de datos**: Asegura que la estructura de la base de datos coincida con los modelos definidos en el código.
6. **Crear las tablas y campos necesarios**: Si es la primera vez que se ejecuta, creará las tablas necesarias en la base de datos basándose en los modelos de Django.

En resumen, `python3 manage.py migrate` mantiene la base de datos actualizada con las definiciones de los modelos en tu proyecto Django.


###### para poder visualizar el archivo `sqlite3`  debemos descargar las *extensiones*  `SQLTools y SQLite Viewer`.


```c
phyton3 manage.py migrate 
```

#### Respuesta des pues de ejecutar:

![[Pasted image 20250206053818.png]]


### 7. ahora ejecutamos el siguiente comando para lanzar el servidor en el localhost:8000


```c
python3 manage.py runserver 
```

**Respuesta exitosa:

![[Pasted image 20250206060450.png]]


### 8.  Rutas con parámetros


**El archivo urls.py:
***En el path adulto tiene el parámetro de edad como lo vemos en la imagen

![[Pasted image 20250206064014.png]]

**Definimos la función con la condicional en el  archivo views.py

![[Pasted image 20250206064215.png]]
***la respuesta que obtenemos con la ruta adulto es siguiendo la instrucción si es mayor o menor de edad :
![[Pasted image 20250206064321.png]]
![[Pasted image 20250206064617.png]]

### 9. Uso de plantillas

https://www.youtube.com/watch?v=KVXdWWcQk_4&list=PLkVpKYNT_U9cl3hhVg_ROOlSY33uuBWZh&index=7
***Establecer cual va ser el directorio donde van a estar las plantillas y archivos html.
***Tenemos el archivo settings. py y en el array de  DIRS se debe poner el nombre de la carpeta en este caso templates:

![[Pasted image 20250206071114.png]]
***Nota: no olvidar descargar la extensión Django para Wsl

***Ahora nos dirigimos a la carpeta `templates` y creamos el archivo `simple.html`:

![[Pasted image 20250206071829.png]]

![[Pasted image 20250206071842.png]]

***La librería de atajos `shortcuts` nos permite renderizar los templates esto lo hacemos en el archivo views.py:

```c
from django.shortcuts import render
```

![[Pasted image 20250206075508.png]]


### 9.  Bucles y condicionales en plantillas

![[Pasted image 20250206232321.png]]

**views.py:

![[Pasted image 20250206232352.png]]



**Resultado:

![[Pasted image 20250206231551.png]]


### 10. Filtros:

 El filtro 'length' se usa para contar la cantidad de elementos en la lista 'models'.En este caso, muestra el total de modelos disponibles.
 
```c
        <h5>Total de modelos: {{models|length}}</h5>
```


![[Pasted image 20250206235327.png]]

***Resultado:

![[Pasted image 20250206235521.png]]


