

---

### 🔁 **1. Obtener todos los elementos**

```python
authors = Author.objects.all()
```

Consulta todos los registros de la tabla `Author`.

---

### 🔎 **2. Filtrar autores por email específico**

```python
filtered = Author.objects.filter(email='derrick12@example.com')
```

Busca todos los autores cuyo email sea exactamente `'derrick12@example.com'`.

---

### 🔍 **3. Obtener un único autor por ID**

```python
author = Author.objects.get(id=1)
```

Busca un autor con `id=1`.  
❗ **Ojo**: si no existe, lanza error (`DoesNotExist`).

---

### 🧮 **4. Obtener los primeros 10 autores**

```python
limits = Author.objects.all()[:10]
```

Trae solo los primeros 10 registros de la base de datos.

---

### ⏭️ **5. Saltar los primeros 5 y traer los siguientes 5**

```python
offsets = Author.objects.all()[5:10]
```

Esto es como paginación manual. Ignora los primeros 5 y muestra del 6 al 10.

---

### 📤 **6. Ordenar autores por email**

```python
orders = Author.objects.all().order_by('email')
```

Ordena todos los autores alfabéticamente por su campo `email`.

---

### 🔢 **7. Filtrar autores con id menor o igual a 15**

```python
filtereds = Author.objects.filter(id__lte=15)
```

Trae solo los autores con `id` menor o igual a 15 (`lte = less than or equal`).

```c
__lte: menor o igual (lower than equals)
__gte: mayor o igual (greater than equals)

__it: menor que (lower than)
__gt: mayor que(greater than)

__contains:contiene
__exact: exacto
```

---

### 📄 **8. Retornar la vista con contexto**

```python
return render(request, 'post/queries.html', {
    'authors': authors,
    'filtered': filtered,
    'author': author,
    'limits': limits,
    'offsets': offsets,
    'orders': orders
})
```

Renderiza el template `post/queries.html` y le envía todas las variables anteriores para que las uses en la plantilla.

---

### ✅ Resumen de para qué sirve

Esta vista es muy útil como **ejemplo educativo o de prueba** para entender cómo hacer consultas en Django: listar, filtrar, paginar, ordenar, etc.



### Documentación Django para la relación de modelos de datos 


- [Many-to-many relationships](https://docs.djangoproject.com/es/5.2/topics/db/examples/many_to_many/)
- [Many-to-one relationships](https://docs.djangoproject.com/es/5.2/topics/db/examples/many_to_one/)
- [One-to-one relationships](https://docs.djangoproject.com/es/5.2/topics/db/examples/one_to_one/)

https://docs.djangoproject.com/es/5.2/topics/db/examples/