

---

## ✅ Modelo `Publication`

```python
class Publication(models.Model):
    title = models.CharField(max_length=30)

    class Meta:
        ordering = ["title"]

    def __str__(self):
        return self.title
```

### 🔍 ¿Qué representa?

- Una publicación o revista donde pueden publicarse artículos.
- Tiene solo un campo: `title`, que es un texto de máximo 30 caracteres.
- `__str__` devuelve el título legible de la publicación.
- `Meta.ordering` hace que, al usar `Publication.objects.all()`, los resultados estén ordenados alfabéticamente por `title`.

---

## ✅ Modelo `Article`

```python
class Article(models.Model):
    headline = models.CharField(max_length=100)
    publications = models.ManyToManyField(Publication)

    class Meta:
        ordering = ["headline"]

    def __str__(self):
        return self.headline
```

### 🔍 ¿Qué representa?

- Un artículo que puede aparecer en una o varias publicaciones.
- `headline`: el título del artículo.
- `publications`: una relación **ManyToMany**, porque:
    - Un artículo puede estar en **varias publicaciones**.
    - Una publicación puede contener **muchos artículos**.

---

### 🔁 ¿Cómo funciona `ManyToManyField`?

Django **crea automáticamente una tabla intermedia** para manejar esta relación. No tienes que definirla tú mismo.

---

## 🔁 Relación entre modelos (resumen)

|Modelo|Relación|Modelo relacionado|
|---|---|---|
|`Article`|ManyToManyField|`Publication`|
|`Publication`|(acceso inverso)|`article_set` (por defecto)|

---

## ✅ Ejemplo práctico en el shell de Django:

```python
# Crear publicaciones
pub1 = Publication.objects.create(title="El País")
pub2 = Publication.objects.create(title="La Nación")

# Crear un artículo
art = Article.objects.create(headline="La inteligencia artificial avanza")

# Asociar el artículo con varias publicaciones
art.publications.add(pub1, pub2)

# Ver publicaciones del artículo
print(art.publications.all())  # <QuerySet [El País, La Nación]>

# Ver artículos publicados en una publicación
print(pub1.article_set.all())  # <QuerySet [La inteligencia artificial avanza]>
```

---

### 📌 Notas importantes:

- Puedes usar `.add()`, `.remove()`, `.set()` y `.clear()` para manipular relaciones muchos a muchos.
- Si necesitas campos adicionales en la relación (como fecha de publicación, autor, etc.), puedes usar un modelo **intermedio** con `through=`.

---

