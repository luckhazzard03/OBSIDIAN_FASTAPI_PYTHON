
## 📌 **Explicación de la Herencia de Plantillas en Django con tu Código**

Django permite **heredar plantillas** usando `{% extends %}` y `{% block %}`, lo que facilita la reutilización de código y la estructura de las páginas.

---

## 🟢 **1. Vistas en `views.py`**

```python
from django.shortcuts import render

def herencia(request):
	return render(request, 'herencia.html', {})

def ejemplo(request):
	return render(request, 'ejemplo.html', {})

def otra(request):
	return render(request, 'otra.html', {})
```

**📌 Explicación:**

- Define **tres funciones** (`herencia`, `ejemplo`, `otra`) que renderizan archivos HTML específicos.
- Cada función usa `render(request, 'archivo.html', {})` para devolver la plantilla correspondiente.

---

## 🟢 **2. Plantilla Base (`base.html`)**

```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="{% static 'style.css' %}">
	{% block styles %}{% endblock %}
	<title>{% block title %}{% endblock %}</title>
</head>
<body>
	<nav>
		<ul>
			<h3>Logo</h3>
			<li><a href="{% url 'herencia' %}">Herencia</a></li>
			<li><a href="{% url 'otra' %}">Otra</a></li>
			<li><a href="{% url 'ejemplo' %}">Ejemplo</a></li>
		</ul>
	</nav>
    <main>
		{% block content %}{% endblock %}
	</main>
	<footer>
		<p>Todos los derechos reservados</p>
	</footer>
	{% block scripts %}{% endblock %}
</body>
</html>
```

**📌 Explicación:**

1. **Carga de archivos estáticos:** `{% load static %}`
2. **Estructura de la página:** HTML con `<head>`, `<body>`, `<nav>`, `<main>`, `<footer>`.
3. **Uso de bloques para herencia:**
    - `{% block styles %}{% endblock %}` → Para agregar CSS en plantillas hijas.
    - `{% block title %}{% endblock %}` → Para definir el título en cada página.
    - `{% block content %}{% endblock %}` → Donde cada plantilla hija insertará su contenido.
    - `{% block scripts %}{% endblock %}` → Para agregar scripts personalizados.

---

## 🟢 **3. Plantillas Hijas**

Ejemplo de `otra.html`:

```html
{% extends "./layouts/base.html" %}

{% block title %}Otra{% endblock %}

{% block content %}
	<h1>Otra</h1>
	<p>Este es un ejemplo de herencia "otra" de plantillas</p>
{% endblock %}
```

**📌 Explicación:**

1. **Hereda de `base.html`** con `{% extends "./layouts/base.html" %}`.
2. **Define el título personalizado:** `{% block title %}Otra{% endblock %}`.
3. **Agrega contenido propio dentro del `{% block content %}`**.

---

## 🟢 **4. Configuración de URLs en `urls.py`**

```python
from django.contrib import admin
from django.urls import path
from . import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('herencia/', views.herencia, name='herencia'),
    path('ejemplo/', views.ejemplo, name='ejemplo'),
    path('otra/', views.otra, name='otra'),
]
```

**📌 Explicación:**

- Cada ruta (`/herencia/`, `/ejemplo/`, `/otra/`) apunta a su función en `views.py`.
- `{% url 'herencia' %}`, `{% url 'otra' %}` en `base.html` usan estos nombres para generar los enlaces automáticamente.

---

## 🟢 **5. Estilos en `style.css`**

```css
/* Global Styles */
body {
	margin: 0;
	padding: 0;
	font-family: Arial, sans-serif;
	background-color: #f4f4f4;
}

/* Header Styles */
header {
	background-color: #333;
	color: #fff;
	padding: 10px 0;
	text-align: center;
}

/* Navigation Styles */
nav {
	background-color: #444;
	color: #fff;
	padding: 10px;
	text-align: center;
}

nav h3 {
	margin: 0 20px 0 0; /* Espacio a la derecha del logo */
	color: #fff;
}

nav ul {
	list-style: none;
	padding: 0;
	margin: 0;
	display: flex;
	justify-content: center;
}

nav li {
	margin: 0 10px;
}

nav a {
	color: #fff;
	text-decoration: none;
}

nav a:hover {
	text-decoration: underline;
}

/* Main Content Styles */
main {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 20px;
	min-height: 80vh;
}

/* Footer Styles */
footer {
	background-color: #333;
	color: #fff;
	text-align: center;
	padding: 50px 0;
	position: fixed;
	bottom: 0;
	width: 100%;
}
```

**📌 Explicación:**

- **Establece un diseño uniforme** para todas las páginas heredadas de `base.html`.
- **Estiliza la navegación (`nav`), el cuerpo (`body`), y el pie de página (`footer`)**.
- **Asegura que el contenido (`main`) se mantenga centrado** y que el footer se quede fijo.

---

## 🎯 **Ventajas de Usar Herencia de Plantillas**

✅ **Código más limpio y organizado** → Se evita la repetición de código HTML.  
✅ **Fácil mantenimiento** → Si cambias `base.html`, todas las páginas hijas se actualizan automáticamente.  
✅ **Mayor flexibilidad** → Cada plantilla hija puede agregar su propio contenido sin afectar la estructura principal.

---

## 🚀 **Resumen**

1. **`base.html` es la plantilla base** con bloques `{% block %}` que las plantillas hijas pueden sobrescribir.
2. **Las plantillas hijas (`otra.html`, `ejemplo.html`) heredan de `base.html`** con `{% extends %}`.
3. **Las vistas (`views.py`) renderizan las plantillas** cuando se accede a sus rutas definidas en `urls.py`.
4. **El CSS en `style.css` se carga en todas las páginas** usando `{% static 'style.css' %}`.
5. **Los enlaces (`{% url 'nombre' %}`) permiten navegar entre páginas sin escribir las rutas manualmente.**

---

