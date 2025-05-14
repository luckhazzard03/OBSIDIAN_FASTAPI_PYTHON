

---
# views.py /comentarios
### 🔹 IMPORTACIONES

```python
from django.shortcuts import render
from django.http import HttpResponse
from .models import Comentario, Usuario, Producto, Pedido
```

- `render`: se usa para devolver plantillas HTML (aunque en este código no se usa directamente).
    
- `HttpResponse`: permite devolver respuestas simples como texto plano.
    
- `.models`: se importan los modelos definidos en tu archivo `models.py`: `Comentario`, `Usuario`, `Producto`, `Pedido`.
    

---

### 🔹 VISTA `test`

```python
def test(request):
    return HttpResponse("Funciona correctamente")
```

- Esta función es una **vista de prueba**.
    
- Cuando accedes a esta ruta, simplemente devuelve el texto `"Funciona correctamente"` en el navegador.
    

---

### 🔹 VISTA `create`

```python
def create(request):
    #comentario = Comentario(name="Juan", score=5, comment="Excelente producto", date="2023-10-01 12:00:00",signature="Firma")
    #comentario.save()
    
    comentario = Comentario.objects.create(
        name="Alex",
        score=5,
        comment="Producto en verificación",
        date="2023-10-01 12:00:00",
        signature="Firma"
    )
    return HttpResponse("Ruta para probar creación de modelos")
```

- Crea un nuevo **comentario** en la base de datos.
    
- Hay dos formas:
    
    - Comentada: creando el objeto con `Comentario(...)` y luego llamando `save()`.
        
    - Usada: con `Comentario.objects.create(...)`, que lo guarda directamente.
        
- Se devuelve una respuesta de confirmación.
    

---

### 🔹 VISTA `delete`

```python
def delete(request):
    #comentario = Comentario.objects.get(id=3)
    #comentario.delete()
    
    Comentario.objects.filter(id=4).delete()
    return HttpResponse("Ruta para probar eliminación de modelos")
```

- Elimina un comentario según su `id`.
    
- Dos formas también:
    
    - Comentada: con `.get()` seguido de `.delete()`.
        
    - Usada: con `.filter().delete()` directamente.
        
- El `id=4` es solo un ejemplo, debes cambiarlo por el ID real de un comentario existente.
    
- Devuelve un mensaje confirmando que se intentó borrar.
    

---

### 📌 En resumen

- Estás creando **rutas simples para probar operaciones básicas con la base de datos**: crear y eliminar registros del modelo `Comentario`.
    
- Esto es útil para probar sin tener que usar el admin de Django o una vista más compleja.
    

---
## settings.py

![[Pasted image 20250505181504.png]]
## urls.py /modularizacion

![[Pasted image 20250505181554.png]]

## urls.py /comentarios
![[Pasted image 20250505181708.png]]