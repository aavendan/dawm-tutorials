..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=============================================================
Django - Django Admin (Autorización)
=============================================================

.. topic:: Objetivo específico
    :class: objetivo

    Configurar el sistema de autenticación y autorización mediante el panel de administración de Django, gestionando usuarios, grupos y permisos de acceso a los endpoints de la API REST, con el propósito de controlar qué acciones pueden realizar distintos perfiles dentro de la aplicación y asegurar el flujo de comunicación de los datos desde usuarios autenticados. 

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

4. Instale las librerías de requirements.txt, con:

   .. code-block:: bash

       pip install -r requirements.txt

Actividades en clases
=====================

Paquete: PyMySQL
-----------------

1. Instale :term:`PyMySQL` en su ambiente de desarrollo:

   .. code-block:: bash

       pip install PyMySQL

2. Utilice su cliente de IAG generativa para explicar el propósito del paquete *PyMySQL* en Python y cómo se utiliza para conectarse a bases de datos MySQL en Django.

Conexión a la base de datos
---------------------------

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

2. En la terminal establezca las variables de entorno para la conexión a la base de datos MySQL, con:

   .. code-block:: bash

       # Linux/MacOS
       export MYSQLDATABASE=security
       export MYSQLUSER=root
       export MYSQLPASSWORD=root
       export MYSQLHOST=localhost
       export MYSQLPORT=3306

       # Verifique las variables de entorno
       echo $MYSQLDATABASE

       # Windows
       set MYSQLDATABASE=security
       set MYSQLUSER=root
       set MYSQLPASSWORD=root
       set MYSQLHOST=localhost
       set MYSQLPORT=3306

       # Verifique las variables de entorno
       echo %MYSQLDATABASE%

   .. note::
      
      Asegúrese de reemplazar los valores con los datos correctos de su base de datos MySQL.

3. Con :term:`MySQL Workbench` o su cliente de MySQL, cree la base de datos **security** si no existe
4. Utilice su cliente de IAG generativa para explicar cómo se configura la conexión a una base de datos MySQL en Django utilizando PyMySQL y las variables de entorno.

Migraciones de base de datos
----------------------------

1. Genere las migraciones de la base de datos, con:

   .. code-block:: bash

       python manage.py makemigrations
       python manage.py migrate

2. Cree un **superusuario** para acceder al panel de administración de Django, con:

   .. code-block:: bash

       python manage.py createsuperuser

3. Cree los usuarios **usuario01** y **usuario02**, sin permisos o pertenencia a algún grupo
4. Levante el servidor de desarrollo, con:

   .. code-block:: bash

       python manage.py runserver

5. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`. 

   .. note:: 
    
       Compruebe que el acceso a la vista principal del dashboard redirige a la vista de inicio de sesión si no está autenticado.

Autorización
------------

Restricción de permiso: decorador `@permission_required`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Edite el archivo ``dashboard/views.py``, con:

   .. code-block:: python
       :emphasize-lines: 2, 5
    
       ...
       from django.contrib.auth.decorators import login_required, permission_required
         
       @login_required
       @permission_required('dashboard.index_viewer', raise_exception=True)
       def index(request):
            ...

2. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`. 

   .. note:: 

      Compruebe que el acceso a la vista principal del dashboard requiere autorización para los usuarios **usuario01** y **usuario02**; mientras, el superusuario tiene acceso sin restricciones.

3. Utilice su cliente de IAG para explicar el uso del decorador `@permission_required` en Django.

Modelo con permisos
^^^^^^^^^^^^^^^^^^^

1. Edite el archivo ``dashboard/models.py``, con la definición del modelo **DashboardModel** con permisos personalizados:

   .. code-block:: python
       :emphasize-lines: 3-8
    
       ...
       # Create your models here.
       class DashboardModel(models.Model):

         class Meta:
            permissions = [
                  ("index_viewer", "Can show to index view (function-based)"),
            ]

2. Genere las migraciones de la base de datos, con:

   .. code-block:: bash
    
       python manage.py makemigrations
       python manage.py migrate

3. Levante el servidor de desarrollo, con:

   .. code-block:: bash

       python manage.py runserver

4. Use el panel de administración de Django `http://127.0.0.1:8000/admin/`, para:

   a) Modificar solo el usuario **usuario01** 
   b) En **User permissions**, agregue el permiso **Dashboard | dashboard model | Can show to index view (function-based)**.
   c) Guarde los cambios.

5. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`.

   .. note:: 
    
       Compruebe que el usuario **usuario01** puede acceder a la vista principal del dashboard, mientras que el usuario **usuario02** recibe un error de autorización; mientras, el superusuario tiene acceso sin restricciones

6. Utilice su cliente de IAG para explicar el uso de los permisos personalizados en modelos de Django y cómo se aplican a las vistas.

403 Forbidden
-------------

1. Descargue y descomprima el archivo :download:`403.zip <./files/exceptions/403.zip>`. 
2. Ubique el archivo ``403.html`` en la carpeta `templates/`.
3. Levante el servidor de desarrollo, con:

   .. code-block:: bash

       python manage.py runserver

4. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`.

   .. note:: 
    
       Compruebe que el usuario **usuario02** recibe un error 403 Forbidden al intentar acceder a la vista principal del dashboard, y que se muestra la plantilla personalizada.


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

   .. info-card:: 

      En caso de tener problemas de autenticación al realizar el versionamiento remoto:
       
      - Obtenga un `Token de acceso personal (clásicos) <https://github.com/settings/tokens>`_ de tipo **Classic**, con el alcance (scope) **repo**.
      - Copie el token, dado que **no podrá volver a verlo**.
      - Borre de memoria cualquier usuario/token que se estuviera guardando temporalmente

        .. code-block:: bash

            git credential-cache exit

      - Elimine la configuración del credential helper definida a nivel global.

        .. code-block:: bash

            git config --global --unset credential.helper

      - Reemplace los valores ``[REPO-OWNER]``, ``[REPO-NAME]`` y ``[TOKEN]`` para modificar el origin.

        .. code-block:: bash
            
            git remote set-url origin https://[REPO-OWNER]:[TOKEN]@github.com/[REPO-OWNER]/[REPO-NAME].git


2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Qué limitaciones identificaste en las soluciones de autenticación sugeridas por la IA, especialmente en relación con la seguridad, la escalabilidad o las buenas prácticas recomendadas por la documentación oficial?

    * ¿Cómo probaste y validaste los mecanismos de autorización implementados, y qué cambios realizaste sobre las configuraciones automáticas para cumplir con los requisitos específicos del proyecto?

    * ¿Qué principios éticos aplicaste al manejar credenciales de usuario y restricciones de acceso en tu backend, especialmente cuando el código base fue propuesto por una IA generativa?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Django is a high-level Python web development framework that lets you build secure, scalable apps.<br><br>And this crash course teaches you the basics so you can start using it.<br><br>You&#39;ll learn about django-admin &amp; <a href="https://t.co/T2lmhj4NZm">https://t.co/T2lmhj4NZm</a>, the Model-View-Template pattern, how forms work,… <a href="https://t.co/G3ZRyfVpb5">pic.twitter.com/G3ZRyfVpb5</a></p>&mdash; freeCodeCamp.org (@freeCodeCamp) <a href="https://twitter.com/freeCodeCamp/status/1919663989262352561?ref_src=twsrc%5Etfw">May 6, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>