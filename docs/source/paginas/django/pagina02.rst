..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=============================================
Django - Server Side Rendering (SSR)
=============================================

.. topic:: Objetivo específico
    :class: objetivo

    Explorar la integración del API REST con aplicaciones que utilizan renderizado del lado del servidor (SSR), evaluando su impacto en el rendimiento, la indexación SEO y la interacción inicial del usuario, con el fin de asegurar una experiencia web optimizada desde el servidor.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *django_backend* en Codespaces o en su máquina local.
2. Cree y utilice la(s) rama(s) de desarrollo.
3. Cree y habilite el ambiente virtual de desarrollo, con:

   .. code-block:: bash

       python -m venv env
       
       env\Scripts\activate # Windows
       source env/bin/activate # Linux/MacOS

4. Instale las dependencias necesarias para el proyecto, con:

   .. code-block:: bash

       python -m pip install -r requirements.txt

5. Levante el servidor de desarrollo de Django:

   .. code-block:: bash

       python manage.py runserver

Actividades en clases
=====================

.. sidebar:: Revisar

   Utilice la `Django - Introducción <https://tutoriales-de-programacion.readthedocs.io/es/latest/paginas/django/pagina01.html>`_ como referencia para la creación del proyecto y la aplicación, creación de vistas con plantillas y configuración de los archivos estáticos.

Dashboard
---------

1. En la raíz del repositorio cree la carpeta `static` y la jerarquía `templates/dashboard`
2. Cree una la aplicación *dashboard* y regístrela a la ruta raíz (\"\").
3. Descargue, descomprima y ubique los archivos en las carpetas correspondientes:

   a) El archivo :download:`base.zip <./files/dashboard/base.zip>`. Ubique el archivo ``base.html`` en la carpeta `templates/dashboard/`.
   b) El archivo :download:`static.zip <./files/dashboard/static.zip>`. Ubique las carpetas dentro de `static/`.

4. Renderice la plantilla ``base.html`` en la vista principal de la aplicación. Configure los archivos estáticos.

   .. note:: 

      Reemplace las rutas de los archivos estáticos en la plantilla por las rutas relativas a la carpeta ``static`` del proyecto.

5. Inicie el servidor de desarrollo y revise los cambios en el navegador en la URL en la ruta raíz la aplicación.
6. Utilice su cliente de IAG generativa para explicar :term:`Server Side Rendering (SSR)` en Django.

Herencia de plantillas
----------------------

1. En el archivo ``templates/dashboard/base.html``, encierre la sección ``Block content`` entre las etiquetas **{% block content %}** y **{% endblock %}**.

   .. code-block:: html      
       :emphasize-lines: 3, 15
      
       ...

       {% block content %}

         <!-- START - Block content -->

            <div class="flex items-center justify-center h-screen bg-gray-100 w-full">
               <div class="p-6 bg-white shadow-md rounded">
                  Block content
               </div>
            </div>
            
         <!-- END - Block content -->

       {% endblock %}

       ...

2. Cree la plantilla `index.html` en la carpeta `templates/dashboard/`, con: 

   a) Extienda de la plantilla `base.html` con la etiqueta **{% extends %}**.
   b) Defina el bloque `content` con la etiqueta **{% block content %}** y **{% endblock %}**, con un título de bienvenida al Dashboard.

   .. code-block:: html
       :emphasize-lines: 1-15

       {% extends "dashboard/base.html" %}

       {% block content %}

         <!-- START - Block content -->
         
            <div class="flex flex-col flex-1 justify-center w-full">

               <h1 class="text-center text-6xl font-bold">Landing Page' Dashboard</h1>

            </div>

         <!-- END - Block content -->
       
       {% endblock %}

3. Renderice la plantilla ``index.html`` en la vista principal de la aplicación *dashboard*.

   .. code-block:: python
       :emphasize-lines: 7

       from django.shortcuts import render

       # Create your views here.
       from django.http import HttpResponse

       def index(request):
           return render(request, 'dashboard/index.html')

4. Revise los cambios en el navegador con la URL raíz.
5. Utilice su cliente de IAG generativa para explicar la :term:`herencia de plantillas` en Django.

Fragmentos de plantilla
-----------------------

1. Descargue los siguientes archivos y ubíquelos en las carpetas correspondientes:

   a) El archivo :download:`header.html <./files/partials/header.html>` en la carpeta `templates/dashboard/partials/` y 
   b) El archivo :download:`data.html <./files/partials/data.html>` en la carpeta `templates/dashboard/content/` .

2. En la plantilla `templates/dashboard/index.html`, reemplace el título por la referencia a los fragmentos de plantilla `header.html` y `data.html`.

   .. code-block:: html
       :emphasize-lines: 9-10

       {% extends "dashboard/base.html" %}

       {% block content %}
       
         <!-- START - Block content -->

            <div class="flex flex-col flex-1 justify-center w-full">

               {% include "./partials/header.html" %}
               {% include "./content/data.html" %}

            </div>

         <!-- END - Block content -->
       
       {% endblock %}

3. Revise los cambios en el navegador con la URL raíz.
4. Utilice su cliente de IAG generativa para explicar los :term:`fragmentos de plantilla` en Django.

Renderización del lado del servidor (SSR)
------------------------------------------

Datos del lado del servidor
^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Edite el archivo ``dashboard/views.py``, con:

   a) Cree un diccionario **data** con el título del Dashboard.
   b) Pase el diccionario como contexto al renderizar la plantilla `index.html`.

   .. code-block:: python
       :emphasize-lines: 6-8, 10

       ...
       from django.http import HttpResponse

       def index(request):

           data = {
               'title': "Landing Page' Dashboard",
           }

           return render(request, 'dashboard/index.html', data)

2. En el fragmento `templates/dashboard/content/data.html`, reemplace el texto **Título Secundario** por la variable **{{ title }}**.

   .. code-block:: html
       :emphasize-lines: 5

       ...
       <h2 class="my-6 text-2xl font-semibold text-gray-700 dark:text-gray-200">

         <!-- START - título secundario -->
         {{ title }}
         <!-- END - título secundario -->

       </h2>
       ...

3. Revise los cambios en el navegador con la URL raíz.
4. Utilice su cliente de IAG generativa para explicar la renderización de datos del lado del servidor en Django.

Respuesta de APIs externas
^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Revise la estructura de la API `JSONPlaceholder <https://jsonplaceholder.typicode.com/posts>`_ y su propósito como un servicio de prueba para simular respuestas de APIs externas.

2. Instale :term:`requests` en su ambiente de desarrollo:

   .. code-block:: bash

       pip install requests

3. Modifique el archivo ``backend_analytics_server/settings.py``, con: 

   a) Agregue la constante **API_URL** con la URL de la API `JSONPlaceholder <https://jsonplaceholder.typicode.com/posts>`_.

   .. code-block:: python
       :emphasize-lines: 2

       ...
       API_URL = 'https://jsonplaceholder.typicode.com/posts'
       ...
4. Edite el archivo ``dashboard/views.py``, con:

   a) Importe el paquete *requests* y el archivo *from django.conf import settings*.
   b) Realice una solicitud GET a la API de `JSONPlaceholder <https://jsonplaceholder.typicode.com/posts>`_ para obtener una lista de publicaciones.
   c) Agregue la entrada **total_responses** al diccionario **data**.

   .. code-block:: python
       :emphasize-lines: 4-5, 9-13, 17

       ...
       from django.http import HttpResponse
       
       import requests
       from django.conf import settings

       def index(request):

           response = requests.get(settings.API_URL)  # URL de la API
           posts = response.json()  # Convertir la respuesta a JSON
           
           # Número total de respuestas
           total_responses = len(posts)

           data = {
               'title': "Landing Page' Dashboard",
               'total_responses': total_responses,
           }

           return render(request, 'dashboard/index.html', data)

5. En el fragmento `templates/dashboard/content/data.html`, reemplace:
 
   a) El texto **Indicador 1** por el texto **Número total de respuestas**, y
   b) El texto **Valor 1** por renderización de la variable **{{ total_responses }}**.


   .. code-block:: html
       :emphasize-lines: 4, 8

       ...
       <div>
         <p class="mb-2 text-sm font-medium text-gray-600 dark:text-gray-400">
            Número total de respuestas
         </p>
         <p class="text-lg font-semibold text-gray-700 dark:text-gray-200">
            <!-- START - valor del indicador 1 -->
            {{ total_responses }}
            <!-- END - valor del indicador 1 -->
         </p>
       </div>
       ...

6. Revise los cambios en el navegador con la URL raíz.

   .. note:: 

      Cambie la variable **API_URL** en el archivo ``settings.py`` con la URL de la **Landing API**.

7. Utilice su cliente de IAG generativa para explicar cómo se manejan las respuestas de APIs externas en Django y cómo se integran en la renderización del lado del servidor.

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

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *django_backend*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Cómo te ayudó la inteligencia artificial generativa a comprender el propósito de la herencia de plantillas y los fragmentos (include) en la construcción de interfaces reutilizables dentro de un sistema de renderizado del lado del servidor como Django?

    * ¿Qué adaptaciones realizaste al código generado por IA para aplicar correctamente la herencia de plantillas y la inclusión de fragmentos sin comprometer la estructura y funcionalidad del backend?

    * ¿Cómo garantizas que el uso de inteligencia artificial no sustituya tu comprensión del flujo completo de renderizado del backend, sino que complemente tu proceso de aprendizaje y diseño como desarrollador en formación?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Rendering on the Web – The SEO Version: Pros and Cons from Server Side to Full Client Side Rendering by <a href="https://twitter.com/jbobbink?ref_src=twsrc%5Etfw">@jbobbink</a> <a href="https://t.co/IioPUtth8Y">https://t.co/IioPUtth8Y</a> <a href="https://t.co/VzZrRGVOOo">pic.twitter.com/VzZrRGVOOo</a></p>&mdash; Aleyda Solis 🕊️ (@aleyda) <a href="https://twitter.com/aleyda/status/1094593901493714945?ref_src=twsrc%5Etfw">February 10, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>