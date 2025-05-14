
---

## 🔹 `from django.db import models`

Esto importa el módulo de Django que permite definir **modelos de base de datos**. Cada clase que hereda de `models.Model` se convierte en una tabla en la base de datos.

---

## 🔹 Modelo `Reporter`

```python
class Reporter(models.Model):
```

Esto crea un modelo llamado `Reporter`, que será una tabla en la base de datos (por ejemplo, `reporter_reporter`).

```python
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
    email = models.EmailField()
```

### 🔍 Explicación de los campos:

- `CharField` define un campo de texto limitado.
- `max_length=30` significa que no puede superar 30 caracteres.
- `EmailField` valida que el contenido ingresado sea un correo electrónico válido.

```python
    def __str__(self):
        return f"{self.first_name} {self.last_name}"
```

### 🔍 ¿Para qué sirve `__str__()`?

Devuelve una representación legible del objeto. Esto es útil, por ejemplo, cuando ves los datos en el **admin de Django** o en la consola.

📌 Ejemplo:

```python
>>> reporter = Reporter(first_name="Ana", last_name="Pérez")
>>> str(reporter)
"Ana Pérez"
```

---

## 🔹 Modelo `Article`

```python
class Article(models.Model):
```

Crea otro modelo, que será otra tabla (por ejemplo, `reporter_article`).

```python
    headline = models.CharField(max_length=100)
    pub_date = models.DateField()
    reporter = models.ForeignKey(Reporter, on_delete=models.CASCADE)
```

### 🔍 Explicación de los campos:

- `headline`: título del artículo, con máximo 100 caracteres.
- `pub_date`: fecha de publicación.
- `reporter`: campo de clave foránea, que **conecta cada artículo con un reportero**.

### 🔁 ¿Qué significa `ForeignKey`?

- Define una **relación uno a muchos**:  
    🔸 **Un solo reportero** puede tener **muchos artículos**,  
    🔸 pero **cada artículo** solo pertenece a **un reportero**.
    
- `on_delete=models.CASCADE`:  
    Si se elimina un `Reporter`, también se eliminarán automáticamente todos sus artículos relacionados.
    

```python
    def __str__(self):
        return self.headline
```

Muestra el **título del artículo** al convertir el objeto a texto.

---

## 🔹 Clase interna `Meta`

```python
    class Meta:
        ordering = ["headline"]
```

### 🔍 ¿Qué hace esto?

Define metadatos del modelo. En este caso:

- **`ordering`** le dice a Django que **cuando consultes múltiples artículos**, los ordene automáticamente por **título (`headline`) en orden alfabético**.

📌 Por ejemplo:

```python
Article.objects.all()
```

Devolverá los artículos ya ordenados por su título (A → Z).

---

## ✅ En resumen

- Tienes dos modelos: `Reporter` y `Article`.
- Cada artículo está conectado a un reportero.
- Se crea una relación uno-a-muchos.
- Se definen representaciones legibles (`__str__`) y ordenamientos automáticos (`Meta.ordering`).
