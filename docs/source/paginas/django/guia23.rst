..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

============================================
Guía 23: Django - Despliegue Python Anywhere
============================================

.. topic:: Objetivo específico
    :class: objetivo

    Desplegar el proyecto Django en la plataforma PythonAnywhere con el fin de publicar el API REST y permitir el acceso remoto a los servicios expuestos, garantizando su disponibilidad como intermediario entre clientes y la base de datos en Firebase Realtime Database.

Actividades previas
=====================

Firebase Admin Python SDK: Clave privada
----------------------------------------

1. En `Firebase Console <https://console.firebase.google.com/>`_, acceda a su proyecto **landing**.
2. Acceda a `Configuración de proyecto` > `Cuentas de servicio` > `SDK de Firebase Admin` para generar la clave privada. 

PythonAnywhere
--------------

1. Obtenga una cuenta Beginner account en `PythonAnywhere <https://www.pythonanywhere.com/>`_.
2. Utilice su cliente de IAG generativa para explicar la utilidad de PythonAnywhere.

Actividades en clases
=====================

PythonAnywhere
--------------

Consola (Console)
^^^^^^^^^^^^^^^^^

1. En PythonAnywhere, acceda a la opción **Consoles**.
2. Cree una nueva consola en **Start a new console:** > **Other: Bash**.
3. Desde la línea de comandos:

   a) Cree un entorno virtual con el nombre environment y con la versión de Python 3.10

   .. code-block:: bash

      mkvirtualenv --python=/usr/bin/python3.10 env

   b) Clone el repositorio *django_api_suite* y acceda a la carpeta *backend_data_server*:

   .. code-block:: bash

      git clone https://github.com/<USUARIO-GITHUB>/django_api_suite.git
      cd django_api_suite

   c) Instale las librerías de requirements.txt, con:

   .. code-block:: bash

       pip install -r requirements.txt

Archivos (Files)
^^^^^^^^^^^^^^^^

Clave privada de Firebase Admin SDK
"""""""""""""""""""""""""""""""""""

1. En PythonAnywhere, acceda a la opción **Files**.
2. Acceda a la carpeta **django_api_suite**.
3. Cree la carpeta **secrets** y suba el archivo de clave privada de Firebase Admin SDK, con el nombre ``landing-key.json``.

Seguridad
"""""""""

4. Edite el archivo ``django_api_suite/backend_data_server/settings.py`` el dominio **ALLOWED_HOSTS** agregue el dominio de su WebApp

   .. code-block:: python
       :emphasize-lines: 2

       ...
       ALLOWED_HOSTS = ['<USUARIO-PYTHONANYWHERE>.pythonanywhere.com']

Archivos estáticos
""""""""""""""""""

5. Edite el archivo ``django_api_suite/backend_data_server/settings.py`` y modifique la configuración de archivos estáticos:

   .. code-block:: python
       :emphasize-lines: 4

       ...
       STATICFILES_DIRS = [ ... ]

       STATIC_ROOT = "assets/"

6. Guarde los cambios en el archivo ``django_api_suite/backend_data_server/settings.py``.

7. Desde la interfaz de Python Anywhere, acceda en la opción **Console** y ejecute el comando:

   .. code-block:: bash

      python manage.py collectstatic

   .. note:: 

      Confirme la creación de la carpeta ``assets`` en la raíz del proyecto.

Aplicación Web (WeApp)
^^^^^^^^^^^^^^^^^^^^^^

1. En PythonAnywhere, acceda a la opción **WebApp**.
2. Seleccione la opción **» Manual configuration (including virtualenvs)**, con la versión de Python 3.10
3. En la interfaz de la WebApp:

   a) En la sección **Virtualenv**, establezca la ruta al entorno virtual ``/home/<USUARIO-PYTHONANYWHERE>/.virtualenvs/env/``.
   b) En el sección **Static files**, relaciona la URL ``/static/`` con la ruta a la carpeta de archivos estáticos ``/home/<USUARIO-PYTHONANYWHERE>/django_api_suite/assets/``.
   c) En la sección **CODE**, haga clic en la opción **Working directory** para modificar la ruta a la carpeta del proyecto ``/home/<USUARIO-PYTHONANYWHERE>/django_api_suite``.
   d) En la sección **CODE**, haga clic en la opción **WSGI configuration file** y reemplace el contenido del archivo con el siguiente código:
     
   .. code-block:: python
      :emphasize-lines: 1-21
    
      # This file contains the WSGI configuration required to serve up your
      # web application at http://<USUARIO-PYTHONANYWHERE>.pythonanywhere.com/
      # It works by setting the variable 'application' to a WSGI handler of some
      # description.
      #
      # The below has been auto-generated for your Django project

      import os
      import sys

      # add your project directory to the sys.path
      project_home = '/home/<USUARIO-PYTHONANYWHERE>/django_api_suite'
      if project_home not in sys.path:
           sys.path.insert(0, project_home)

      # set environment variable to tell django where your settings.py is
      os.environ['DJANGO_SETTINGS_MODULE'] = 'backend_data_server.settings'

      # serve django via WSGI
      from django.core.wsgi import get_wsgi_application
      application = get_wsgi_application()

   .. note:: 
        
      Reemplace `<USUARIO-PYTHONANYWHERE>` con su nombre de usuario en PythonAnywhere.    
    
   e) Guarde los cambios en el archivo ``wsgi.py``.

4. En la sección **Web**, haga clic en el botón **Reload** para reiniciar la WebApp y aplicar los cambios.
5. Revise los cambios en el navegador en la URL: `http://<USUARIO-PYTHONANYWHERE>.pythonanywhere.com/`.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Qué aprendiste sobre el funcionamiento de un entorno de despliegue en la nube como PythonAnywhere gracias al uso de inteligencia artificial generativa, y qué conceptos necesitaste investigar más allá del código generado?

    * ¿Cómo verificaste que tu backend estuviera correctamente desplegado y accesible desde un entorno externo, y qué medidas tomaste para solucionar problemas derivados de configuraciones automatizadas?

    * ¿Cómo te aseguras de que el uso de inteligencia artificial en el despliegue no limite tu comprensión del proceso ni te impida desarrollar autonomía técnica como desarrollador backend?


Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Top 5 Reasons Why PythonAnywhere Should Be Your Next Project&#39;s Home<br><br>1. Zero Setup Hassle<br>2. Collaboration Made Easy<br>3. Always Available, Anywhere Access<br>4. Scales With Your Needs<br>5. Fantastic for Web Apps<br><br>Over to you: What are your go-to tools for Python development? <a href="https://twitter.com/hashtag/python?src=hash&amp;ref_src=twsrc%5Etfw">#python</a> <a href="https://t.co/je9mAEH0jf">pic.twitter.com/je9mAEH0jf</a></p>&mdash; DavidayoTech (@DavidayoAI) <a href="https://twitter.com/DavidayoAI/status/1872787250838376602?ref_src=twsrc%5Etfw">December 27, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>