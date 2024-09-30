#DJANGO #Python 
![[Pasted image 20240926095037.png]]

### En Django, se utilizan expresiones regulares para definir, extraer.

![[Pasted image 20240926095424.png]]

![[Pasted image 20240926100024.png]]
# Vistas y espacios de nombres de URL
#vistasEspaciosURL
 
Esta lectura explica el uso de URL con nombre en la ``URLconf`` de una aplicación Django y cómo el uso de un espacio de nombres ayuda a resolver el mismo nombre de URL en más de una aplicación.

En cada aplicación, existe un archivo urls.py que define la lista de patrones de URL para esa aplicación. Cada patrón lo construye la función ``django.urls.path()``. Sus argumentos son una cadena de ruta de URL, el nombre de la función de vista que se le asignará y un nombre de argumento opcional.

El siguiente es el ``urls.py`` de una aplicación:

```c
#demoapp/urls.py 
from django.urls import path 
from . import views 

  

  urlpatterns = [ 
    path('', views.index, name='index'), 
    path('login/', views.login, name='login') 

]
```

Está incluido en los patrones url del proyecto.

```c
from django.contrib import admin 
from django.urls import path, include   

  urlpatterns = [ 
    path('admin/', admin.site.urls), 
    path('demo/', include('demoapp.urls')), 

]
```

Normalmente, la URL de solicitud del cliente se asigna a la función para que el flujo de la aplicación se dirija hacia ella.

Las referencias URL utilizadas internamente por la aplicación son cadenas codificadas de forma rígida.

Por ejemplo, el atributo de acción de una plantilla de formulario apunta hacia ``/demoapp/login ``URL para que cuando se envíe el formulario, se invoque la vista de inicio de sesión asignada a esta URL.

```c
<form action='/demoapp/login', method='POST> 
    # ...
</form>
```

## Función _reverse()_ (inversa)

Sin embargo, las URL codificadas hacen que la aplicación sea menos escalable y difícil de mantener a medida que crece el proyecto. En tal caso, puede obtener la URL del parámetro de nombre utilizado en la función ``path() (ruta)``.

Inicie el shell de Django.

```c
python manage.py shell
```

La función reverse() (inversa) de Django devuelve la ruta URL a la que está asignada.

```c
>>> from django.urls import reverse 
>>> reverse('index') 
'/demo/'
```


El problema surge cuando la función de vista del mismo nombre está definida en más de una aplicación. Aquí es donde se necesita la idea de un espacio de nombres.


## Espacio de nombres de la aplicación

El espacio de nombres de la aplicación se crea mediante la variable ``app_name`` en el archivo ``urls.py`` de la aplicación y asignándole el nombre de la aplicación. En el script ``demoapp/urls.py``, realice el cambio mediante el siguiente código:

```c
#demoapp/urls.py
from django.urls import path  
from . import views    

app_name='demoapp'
urlpatterns = [  
    path('', views.index, name='index'),    

]
```

``app_name`` define el espacio de nombres de la aplicación para que identifique las vistas en esta aplicación.

Para obtener la ruta URL de la función ``index() (índice)``, llame a la función ``reverse() (inversa``) anteponiéndole el espacio de nombres.


```c
>>> reverse('demoapp:index') 
'/demo/'
```


Para apreciar la ventaja de definir un espacio de nombres, agregue otra aplicación en el proyecto, por ejemplo, ``newapp (aplicación nueva)``. Proporcione una función de vista ``index()`` en él y defina ``app_name`` en su archivo URLConf (es decir, ``urls.py``).

```c
#newapp/urls.py 

from django.urls import path 
from . import views 

app_name='newapp' 
urlpatterns = [ 
    path('', views.index, name='index'),
]
```

Actualice el ``urls.py``. del proyecto.

```c
from django.contrib import admin 
from django.urls import path, include 
  

urlpatterns = [ 
    path('admin/', admin.site.urls), 
    path('demo/', include('demoapp.urls')),
    path('newdemo/', include('newapp.urls')), 

]
```

La función ``reverse()`` ``(inversa)`` se ejecuta para la vista de índice en el espacio de nombres ``newapp (aplicación nueva)``.

```c
>>> reverse('newapp:index') 
'/newdemo/'
```

Puede ver que Django diferencia entre URL con el mismo nombre en varias aplicaciones con espacio de nombres de aplicación.


## Espacio de nombres de instancia

También puede usar el parámetro de espacio de nombres en la función`` include() (incluir)`` al agregar el patrón de URL de una aplicación al de un proyecto.


```c
#in demoproject/urls.py 

urlpatterns=[ 
    # ... 

    path('demo/', include('demoapp.urls', namespace='demoapp')), 

    # ... 

]
```

Este espacio de nombres se denomina espacio de nombres de instancia.

## Uso del espacio de nombres en la vista

Suponga que desea que el usuario sea redirigido condicionalmente a la vista de inicio de sesión desde dentro de otra vista.

Debe obtener la URL de la vista de inicio de sesión y enviarle el control con HttpResponsePermanentRedirect.


```c
from django.http import HttpResponsePermanentRedirect 
from django.urls import reverse 

def myview(request): 
    .... 
    return HttpResponsePermanentRedirect(reverse('demoapp:login'))
```


## espacio de nombres en la etiqueta de url

Se envía un formulario HTML a la URL especificada en el atributo de acción.


```c
<form action="/demoapp/login" method="post">   

#form attributes  

<input type='submit'>   

</form>
```


Luego, la vista asignada a esta URL procesará el formulario. Sin embargo, como se mencionó anteriormente, no se desea una URL codificada. En su lugar, utilice la etiqueta url del lenguaje de plantillas de Django. Devuelve la ruta absoluta de la URL nombrada.

Utilice la etiqueta de url para obtener la ruta de la URL de forma dinámica, como se muestra a continuación:

```c
<form action="{% url 'login' %}" method="post">
#form attributes 
<input type='submit'> 
</form>
```


Una vez más, la vista de inicio de sesión puede estar presente en varias aplicaciones. Utilice la URL con nombre calificada con el espacio de nombres para resolver el conflicto.

```c
<form action="{% url 'demoapp:login' %}" method="post"> 
#form attributes 
<input type='submit'>
</form>
```

El navegador muestra el formulario de inicio de sesión como se muestra a continuación:

![[Pasted image 20240926101823.png]]

Por lo tanto, el concepto de espacio de nombres ayuda a resolver el conflicto que surge de varias aplicaciones en el mismo proyecto que tienen vistas del mismo nombre.

Ha cubierto algunos de los conceptos aquí en línea con el uso de plantillas de formulario en Django. Si tiene dificultad para comprender algunas cosas, tenga la seguridad de que será mucho más claro una vez que cubra el tema de las plantillas en este curso.

En esta lectura, exploró más a fondo el concepto de espacio de nombres de URL y vistas en Django.


# Solución: Creación de direcciones URL y asignación a vistas