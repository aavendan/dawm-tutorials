..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=======================================
Django - Despliegue en Railway
=======================================

.. topic:: Objetivo específico
    :class: objetivo

    Realizar el despliegue de un proyecto Django en la plataforma Railway para la publicación de un servicio web accesible desde cualquier cliente y garantizar la comunicación estable y segura con los datos. 

Actividades previas
=====================

Ambiente de producción
----------------------

1. Acceda a su proyecto *django_backend* en Codespaces o en su máquina local.
2. Cree y utilice la rama de **produccion**.
3. Cree y habilite el ambiente virtual, con:

   .. code-block:: bash

       python -m venv env
       
       env\Scripts\activate # Windows
       source env/bin/activate # Linux/MacOS

4. Instale las librerías de requirements.txt, con:

   .. code-block:: bash

       pip install -r requirements.txt

Actividades en clases
=====================

Paquete: gunicorn y whitenoise
------------------------------

1. Instale `PyMySQL`, :term:`gunicorn` y :term:`whitenoise` en su ambiente, con:

   .. code-block:: bash
    
       pip install gunicorn whitenoise PyMySQL

2. Utilice su cliente de IAG generativa para explicar la utilidad de los paquetes gunicorn y whitenoise.

Configuración de Django para producción
---------------------------------------

Conexión a la base de datos (Obligatorio)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Edite el archivo ``backend_analytics_server/settings.py`` de su proyecto Django, con:

   a) Importe el paquete PyMySQL:

   .. code-block:: python
       :emphasize-lines: 4-6

       ...
       from pathlib import Path
       import os
       import pymysql

       pymysql.install_as_MySQLdb()
       
       ...

   b) Reemplace la configuración por defecto por la conexión a la base de datos MySQL utilizando PyMySQL:

   .. code-block:: python
       :emphasize-lines: 5-10

       ...

       DATABASES = {
           'default': {
               'ENGINE': 'django.db.backends.mysql',
               'NAME': os.environ.get('MYSQLDATABASE'),
               'USER': os.environ.get('MYSQLUSER'),
               'PASSWORD': os.environ.get('MYSQLPASSWORD'),
               'HOST': os.environ.get('MYSQLHOST'),
               'PORT': os.environ.get('MYSQLPORT'),
            }
       }

       ...

Conexión a la base de datos
^^^^^^^^^^^^^^^^^^^^^^^^^^^

2. En el archivo `backend_analytics_server/settings.py`, configure los siguientes parámetros:

   a) **DEBUG**: Cambie a `False`.
   b) **CSRF_TRUSTED_ORIGINS**: Agregue el dominio de Railway.
   c) **ALLOWED_HOSTS**: Utilice el dominio de Railway.
   d) **MIDDLEWARE**: Agregue el :term:`middleware` `WhiteNoiseMiddleware` para servir archivos estáticos.
   e) **STATIC_ROOT**: Configure la ruta para los archivos estáticos
   f) **STATICFILES_STORAGE**: Configure el almacenamiento de archivos estáticos

   .. code-block:: python
       :emphasize-lines: 1,4,8,12,21,23

       DEBUG = False
       
       CSRF_TRUSTED_ORIGINS = [
           "https://*.up.railway.app",
           ...,
       ]

       ALLOWED_HOSTS = ['.up.railway.app']
       
       MIDDLEWARE = [
          'django.middleware.security.SecurityMiddleware',
          'whitenoise.middleware.WhiteNoiseMiddleware',  # Agregar WhiteNoise al middleware (debe ir después de SecurityMiddleware)
          'django.contrib.sessions.middleware.SessionMiddleware',
           # ... resto de middlewares
       ]

       ...

       STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]

       STATIC_ROOT = BASE_DIR / 'assets' 

       STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
       
       ...

Gestión de dependencias y versionamiento
----------------------------------------

1. Genere el archivo `requirements.txt` con la lista de paquetes utilizados, con:

   .. code-block:: bash

       pip freeze > requirements.txt

2. Desactive el ambiente virtual de desarrollo, con:

   .. code-block:: bash

       deactivate

3. Versione local y remotamente la rama **produccion**.


Railway
-------

1. Obtenga una cuenta gratuita en `Railway <https://railway.app/>`_ mediante su cuenta de GitHub.
2. Cree un proyecto nuevo vacío.
3. Utilice su cliente de IAG generativa para explicar la utilidad de Railway.

Configuración en Railway
------------------------

Servicio: MySQL Database
^^^^^^^^^^^^^^^^^^^^^^^^^

1. En Railway, acceda al proyecto vacío.
2. Seleccione la opción **Add Service**, escoja **Database** y luego **Add MySQL**.

Servicio: Web App
^^^^^^^^^^^^^^^^^

1. En Railway, dentro del proyecto.
2. Seleccione **Create** > **GitHub Repo** y conecte su cuenta de GitHub.
3. Seleccione el repositorio *django_backend*. 

   .. attention::
      
      No despliegue la aplicación hasta configurar correctamente las variables de entorno.

4. En la pestaña **Environment Variables**, configure:

   a) Agregue las 5 referencias a las variables `MYSQLDATABASE`, `MYSQLUSER`, `MYSQLPASSWORD`, `MYSQLHOST` y `MYSQLPORT` con sus valores correspondientes al servicio de MySQL, por ejemplo:

   .. code-block:: bash

       MYSQLDATABASE     ${{MySQL.MYSQLDATABASE}}

   b) Agregue las 3 variables `DJANGO_SUPERUSER_USERNAME`, `DJANGO_SUPERUSER_PASSWORD` y `DJANGO_SUPERUSER_EMAIL` con sus valores para crear el superusuario.

   .. code-block:: bash

       DJANGO_SUPERUSER_EMAIL     admin@data.com.ec

5. En la pestaña **Settings**, configure el entorno de producción:

   a) Seleccione la rama **produccion**
   
   b) En **Build** > **Custom Build Command**, utilice:

   .. code-block:: bash

       pip install -r requirements.txt

   c) En **Deploy** > **Custom Start Command**, utilice:

   .. code-block:: bash

       gunicorn backend_analytics_server.wsgi
   
   d) En **Deploy** > **Pre-deploy Step**, utilice:

   .. code-block:: bash

       python manage.py makemigrations && python manage.py migrate && python manage.py collectstatic --noinput && python manage.py createsuperuser --noinput

5. Haga clic en el botón **Deploy** para desplegar los servicios con los cambios realizados.
6. Luego del despliegue exitoso, **Setting** > **Networking**, genere un dominio en el puerto 8080.
7. Revise los registros de despliegue para asegurarse de que no haya errores.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Qué elementos clave del proceso de despliegue en Railway comprendiste mejor gracias a la inteligencia artificial generativa, y qué conceptos tuviste que reforzar por tu cuenta para asegurar una implementación funcional?

    * ¿Cómo verificaste el funcionamiento correcto del backend desplegado en Railway, y qué hiciste para resolver problemas como errores de conexión a la base de datos o fallas en el entorno de producción?

    * ¿Qué actitudes asumiste para garantizar que el uso de inteligencia artificial en el proceso de despliegue no reemplazara tu comprensión del entorno de producción, sino que fortaleciera tu capacidad como desarrollador responsable?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Drop the .app, it&#39;s cleaner that way <br><br>Introducing an all-new Railway (dot com)<a href="https://t.co/C5PSPyo5IO">https://t.co/C5PSPyo5IO</a></p>&mdash; Railway (@Railway) <a href="https://twitter.com/Railway/status/1857148311494623725?ref_src=twsrc%5Etfw">November 14, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>