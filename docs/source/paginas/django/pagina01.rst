..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

==============================
Django - Introducción
==============================

.. topic:: Objetivo específico
    :class: objetivo

    Introducir al uso del framework Django para el desarrollo backend con el fin de establecer una base sólida que permita construir una aplicacion de backend estructurada y escalable. 

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Cree un repositorio en GitHub con el nombre *django_api_suite*.

   a) Agregue un archivo README.md con el título de su backend y una breve descripción del objetivo de su proyecto.
   b) Agregue un archivo *.gitignore* con la plantilla de *Python*.
   
2. Acceda a su proyecto *django_api_suite* en Codespaces o en su máquina local.
3. Cree y utilice la(s) rama(s) de desarrollo.
4. Cree y habilite el :term:`ambiente virtual de desarrollo`, con:

   .. code-block:: bash

       python -m venv env
       source env/bin/activate

   .. note:: 
      
      Revise las instrucciones para `habilitar el ambiente de desarrollo <https://docs.python.org/3/tutorial/venv.html#tut-venv>`_ para su sistema operativo.

Actividades en clases
=====================

Paquete: Django
---------------

1. Instale :term:`Django` en su ambiente de desarrollo:

   .. code-block:: bash
    
       pip install django

2. Utilice su cliente de IAG generativa para explicar qué es Django, cuáles son sus principales características y los patrones de diseño que implementa.

Proyecto: Backend Data Server
-----------------------------

1. Cree un :term:`proyecto Django` llamado *backend_data_server* en la ubicación actual, sin crear una aplicación:

   .. code-block:: bash

       django-admin startproject backend_data_server .

2. Levante el servidor de desarrollo de Django:

   .. code-block:: bash

       python manage.py runserver

3. Revise los cambios en el navegador en la :term:`URL raíz`.
4. Utilice su cliente de IAG generativa para explicar la estructura de archivos de un proyecto en Django.

Aplicación: Homepage
--------------------

Creación de la aplicación
^^^^^^^^^^^^^^^^^^^^^^^^^

1. Cree una :term:`aplicación Django` llamada *homepage*, con:

   .. code-block:: bash

       python manage.py startapp homepage

Registro de la aplicación
^^^^^^^^^^^^^^^^^^^^^^^^^

2. Registre la aplicación en el archivo de configuración ``backend_data_server/settings.py`` del proyecto:

   .. code-block:: python
      :emphasize-lines: 3

      INSTALLED_APPS = [
        ...
        "homepage",
      ]

3. En el archivo ``backend_data_server/urls.py``, importe el módulo **include** y asocie la ruta \"homepage/\" con las subrutas de la aplicación **homepage**:

   .. code-block:: python
      :emphasize-lines: 2, 6

      from django.contrib import admin
      from django.urls import path, include

      urlpatterns = [
         path("admin/", admin.site.urls),
         path("homepage/", include("homepage.urls")),
      ]

Rutas y Vistas de la aplicación
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

4. Cree el archivo ``homepage/urls.py`` con las rutas de la aplicación:

   .. code-block:: python
      :emphasize-lines: 1-6

      from django.urls import path
      from . import views

      urlpatterns = [
         path("index/", views.index, name="index"),
      ]

5. Cree la :term:`vista basada en funciones` en ``homepage/views.py`` que retorne un mensaje de bienvenida:

   .. code-block:: python
      :emphasize-lines: 4-7

      from django.shortcuts import render

      # Create your views here.
      from django.http import HttpResponse

      def index(request):
          return HttpResponse("¡Bienvenido a la aplicación Django!")

6. Levante el servidor de desarrollo de Django:

   .. code-block:: bash

       python manage.py runserver

7. Revise los cambios en el navegador con la URL raíz, seguida por la ruta `/homepage/index/`
8. Utilice su cliente de IAG generativa para explicar la estructura de archivos de una aplicación, en el contexto de Django.
   
   .. note:: 

      Para que su sitio web responda a la URL raíz, asocie la ruta vacía (\"\") del proyecto con la aplicación **homepage** y la ruta vacía (\"\") de la aplicación con la vista **index**.

SSR: Plantillas
---------------

.. sidebar:: 

   Django implementa la técnica web de desarrollo :term:`Server Side Rendering (SSR)` donde el servidor web genera el HTML para una página web y lo envía como una página completamente renderizada al cliente (navegador).

1. En la raíz del repositorio, cree la jerarquía de carpetas ``templates/homepage`` 
2. Descargue el archivo :download:`index.html <./files/homepage/index.html>` y colóquelo en la carpeta ``templates/homepage``.
3. Modifique el archivo ``backend_data_server/settings.py`` 

   a) Importe el módulo **os**
   b) Agregue la ruta a las plantillas en el arreglo **TEMPLATES**, en la entrada **DIRS**.

   .. code-block:: python
      :emphasize-lines: 2, 9

      from pathlib import Path
      import os

      ... 

      TEMPLATES = [
          {
              ...
              "DIRS": [os.path.join(BASE_DIR, 'templates')],
              ...
          },
      ]

4. Edite el archivo ``homepage/views.py``:

   a) Agregue la renderización de la plantilla ``homepage/index.html`` en la vista `index`:

   .. code-block:: python
      :emphasize-lines: 4-5

      from django.shortcuts import render

      def index(request):
          # return HttpResponse("¡Bienvenido a la aplicación Django!")
          return render(request, 'homepage/index.html')

5. Revise los cambios en el navegador en la URL en la ruta de la aplicación.
6. Utilice su cliente de IAG generativa para explicar la renderización de plantillas en Django.

   .. note:: 

      La plantilla original se encuentra en el repositorio de GitHub `Windmill Dashboard <https://github.com/estevanmaito/windmill-dashboard>`_, con la vista previa en `Windmill Dashboard <https://windmill-dashboard.vercel.app/>`_.

Archivos estáticos
------------------

1. En la raíz del repositorio, cree la jerarquía de carpetas ``static/img``  
2. Descargue el archivo :download:`team.jpg <./files/homepage/team.jpg>` y colóquelo en la carpeta ``static/img``.
3. Edite el archivo ``backend_data_server/settings.py``, 

   a) Agregue el arreglo **STATICFILES_DIRS** con la ruta a la carpeta de archivos estáticos:

   .. code-block:: python
      :emphasize-lines: 3-5

      STATIC_URL = "static/"

      STATICFILES_DIRS = [
          os.path.join(BASE_DIR, STATIC_URL),
      ]

4. Edite el archivo ``templates/homepage/index.html``:

   a) Agregue la etiqueta **{% load static %}** al inicio del archivo.
   b) Reemplace las rutas de los archivos estáticos por las etiquetas **{% static '...' %}**.

   .. code-block:: html
      :emphasize-lines: 1, 13, 16

      {% load static %}

      <!DOCTYPE html>
      <html lang="en">
      <head>
          ...
      </head>
      <body>
      
          ...
          
          <img aria-hidden="true" class="object-cover w-full h-full dark:hidden" 
                src="{% static '/img/team.jpg' %}"
                alt="Office" />
           <img aria-hidden="true" class="hidden object-cover w-full h-full dark:block" 
                src="{% static '/img/team.jpg' %}"
                alt="Office" />

          ...
      </body>
      </html>

5. Revise los cambios en el navegador en la URL en la ruta de la aplicación.
6. Utilice su cliente de IAG generativa para explicar la utilidad de la etiqueta **{% load static %}** y el uso **{% static '...' %}** en Django.

Gestión de dependencias
-----------------------

1. Genere el archivo `requirements.txt` con la lista de paquetes utilizados, con:

   .. code-block:: bash

       pip freeze > requirements.txt

2. Desactive el ambiente virtual de desarrollo, con:

   .. code-block:: bash

       deactivate

Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *django_api_suite*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Cómo te ayudó la IA a diferenciar entre el propósito de un proyecto y el de una aplicación dentro de Django, y por qué es importante esa distinción en el desarrollo modular del backend?

    * ¿Cómo estructuraste los archivos estáticos y plantillas en tu proyecto para lograr una arquitectura clara, eficiente y reutilizable, y qué papel jugó la IA en ese proceso de diseño?

    * ¿Cómo mantuviste tu rol activo y reflexivo durante el proceso de aprendizaje, evitando depender exclusivamente del código generado por la IA para configurar tu proyecto Django?


Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="es" dir="ltr">Si te gusta Python, en este artículo se comparan pros y contras de algunos de los frameworks de desarrollo web más potentes.<br><br>Reflex vs Django vs Flask vs Gradio vs Streamlit vs Dash vs FastAPI<br><br>→ <a href="https://t.co/PiQFOqWWEx">https://t.co/PiQFOqWWEx</a> <a href="https://t.co/3zXjrKsVa4">pic.twitter.com/3zXjrKsVa4</a></p>&mdash; Brais Moure (@MoureDev) <a href="https://twitter.com/MoureDev/status/1870839215161840071?ref_src=twsrc%5Etfw">December 22, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>