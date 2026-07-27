..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

==============================================
Django - Django Admin (Autenticación)
==============================================

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

Migraciones de base de datos
----------------------------

1. Genere las migraciones de la base de datos, con:

   .. code-block:: bash

       python manage.py makemigrations
       python manage.py migrate

2. Cree un **superusuario** para acceder al panel de administración de Django, con:

   .. code-block:: bash

       python manage.py createsuperuser


3. Utilice su cliente de IAG para explicar las migraciones de base de datos, el uso del panel de administración de Django y el propósito del superusuario.

Configuración de dominios y CSRF
---------------------------------

1. Modifique el archivo ``django_backend/settings.py``, con:

   .. code-block:: python
       :emphasize-lines: 2-6, 8-10

       ...
       CSRF_TRUSTED_ORIGINS = [
         "https://*.app.github.dev", # Solo si utiliza Codespaces
         "https://localhost:8000",
         "http://127.0.0.1:8000"
       ]

       ALLOWED_HOSTS = [
         "*",
       ]
       ...

   .. note::

       El uso de `ALLOWED_HOSTS` con el valor `['*']` es una práctica insegura para producción, pero es aceptable para desarrollo local. En producción, se debe especificar el dominio o subdominio del servidor.

2. Levante el servidor de desarrollo, con:

   .. code-block:: bash

       python manage.py runserver


3. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/admin/`. Inicie sesión con las credenciales del superusuario y explore el panel de administración.
4. Cree los usuarios **usuario01** y **usuario02**, sin permisos o pertenencia a algún grupo.
5. Utilice su cliente de IAG para explicar la configuración de `ALLOWED_HOSTS` y `CSRF_TRUSTED_ORIGINS`.

Autenticación
-------------

Restricción de acceso: decorador `@login_required`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Edite el archivo ``dashboard/views.py``, con:

   .. code-block:: python
       :emphasize-lines: 2, 4
    
       ...
       from django.contrib.auth.decorators import login_required
         
       @login_required
       def index(request):
            ...

2. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`. 

   .. note:: 

      Compruebe que el acceso a la vista principal del dashboard requiere autenticación, al mostrar el formulario de inicio de sesión.

3. Utilice su cliente de IAG para explicar el uso del :term:`decorador` `@login_required` en Django.

Login: Vista y Plantilla de autenticación
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Descargue y descomprima el archivo :download:`login.zip <./files/security/login.zip>`. Ubique el archivo ``login.html`` en la carpeta `templates/security/`.
2. Modifique el archivo ``django_backend/urls.py``, con:

   a) Importe las vistas predefinidas auth_views.
   b) Agregue las rutas con las vista (basadas en clases) asociadas con el inicio (LoginView) y con el cierre (LogoutView) de sesión.

   .. code-block:: python
      :emphasize-lines: 2, 7-8, 10-11

      ...
      from django.contrib.auth import views as auth_views

      urlpatterns = [
        ...

        # Ruta login/ para la vista LoginView para inicio de sesión, uso de plantilla y alias
        path('login/', auth_views.LoginView.as_view(template_name='security/login.html'), name='login'),
            
        # Ruta logout/ para la vista LogoutView para fin de sesión, redirección y alias
        path('logout/', auth_views.LogoutView.as_view(next_page='/login/'), name='logout'),

      ]

3. Modifique el archivo ``django_backend/settings.py``, con:

   a) Agregue la constante **LOGIN_URL** con la URL de inicio de sesión.
   b) Agregue la constante **LOGOUT_REDIRECT_URL** con la URL raíz del proyecto.
    
   .. code-block:: python
       :emphasize-lines: 2-3, 5-6
    
       ...
       # Fallo: acceso sin autenticación
       LOGIN_URL = '/login/'

       # Éxito: luego de autenticación exitosa
       LOGIN_REDIRECT_URL = '/'


4. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`. 

   .. note:: 
    
       Compruebe que el acceso a la vista principal del dashboard redirige a la vista de inicio de sesión si no está autenticado.

5. Utilice su cliente de IAG para explicar el uso de las vistas predefinidas `LoginView` y `LogoutView` en Django, así como la configuración de las constantes `LOGIN_URL` y `LOGOUT_REDIRECT_URL`.
        
Inicio de sesión
^^^^^^^^^^^^^^^^

1. Edite el archivo ``templates/security/login.html``, con:

   a) Agregue el método **post** y el atributo **action** con la URL de inicio de sesión (alias 'login'),
   b) Agregue el :term:`token CSRF` para proteger el formulario,
   c) Agregue el atributo **name** a los campos de entrada para el nombre de usuario y la contraseña.

   .. code-block:: html
       :emphasize-lines: 3, 6, 10, 14

       ...
       <!-- Método post y action para el URL (con el alias 'login') -->
       <form method="post" action="{% url 'login' %}">

            <!-- CSRF token -->
            {% csrf_token %}
            ...

            <!-- username -->
            <input name="username" ... >
            ...

            <!-- password -->
            <input name="password" ... >
            ...
       </form>

2. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`. 

   .. note:: 

      Compruebe que la autenticación con las credenciales de los usuarios **superusuario**, **usuario01** y **usuario02**, se redirija al usuario a la vista principal del dashboard. Y que la autenticación con las credenciales incorrectas redirige al usuario a la vista de inicio de sesión.

3. Utilice el inspector del navegador para verificar la :term:`cookie de sesión`.

Fin de sesión
^^^^^^^^^^^^^

1. Modifique ``templates/dashboard/partials/header.html`` en el bloque **logout**, con:

   .. code-block:: html
       :emphasize-lines: 5, 8

       ...
       <!-- START - Block Logout -->
    
       <!-- Método post y action para el URL (con el alias 'logout') -->
       <form method="post" action="{% url 'logout' %}" class="w-full">

            <!-- CSRF token -->
            {% csrf_token %}

            ...

       </form>
       <!-- END - Block Logout -->
       ...

2. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`.

   .. note:: 

      Compruebe que el cierre de sesión redirige al usuario a la vista de inicio de sesión.

3. Utilice su cliente de IAG para explicar el uso del `token CSRF` en Django y el uso de la `cookie de sesión`.

Verificación de acceso
----------------------

Escenario: Acceso fallido
^^^^^^^^^^^^^^^^^^^^^^^^^

1. Modifique el archivo ``templates/security/login.html``, con:

   .. code-block:: html
       :emphasize-lines: 4-8

       ...
       <div class="w-full">
         
         {% if form.non_field_errors %}
                                 
            <div id="password_error_div" class="flex items-center justify-center mb-4 py-3 bg-red-100 border-l-4 border-red-500 text-red-700 dark:border-red-400 dark:text-red-500" role="alert">Invalid username or password.</div>
         
         {% endif %}

         <!-- Método post y action para el URL (con el alias 'login') -->
         <form method="post" action="{% url 'login' %}">
         ...
         </form>
         
         ...
       </div>
       
Escenario: Acceso exitoso
^^^^^^^^^^^^^^^^^^^^^^^^^

2. Modifique el archivo ``templates/partials/header.html``, con:

   .. code-block:: html
       :emphasize-lines: 6-10

       ...

       <!-- Profile menu -->
       <li class="relative">
         
         {% if user.is_authenticated %}
            
            <span>{{ user.username }}</span>

         {% endif %}

         <button ... > ... </button>
       </li>

       ...

3. Revise los cambios en el navegador con la URL `http://127.0.0.1:8000/`.

   .. note::

      Compruebe que la autenticación con un usuario no registrado muestra el mensaje de error "Invalid username or password." y que la autenticación con un usuario registrado muestra el nombre de usuario en el menú de perfil.

4. Utilice su cliente de IAG para explicar el uso la etiqueta de plantilla ``{% if %} ... {% endif %}`` y los objetos **form** y **user** en Django.

Gestión de dependencias
-----------------------

1. Genere el archivo `requirements.txt` con la lista de paquetes utilizados, con:

   .. code-block:: bash

       pip freeze > requirements.txt

2. Desactive el ambiente virtual de desarrollo, con:

   .. code-block:: bash

       deactivate


.. warning::

   Asegúrese que el ``.gitignore`` contenga el nombre del archivo ``db.sqlite3``, para no versionar la base de datos en su repositorio.

Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *django_data_monitor*.


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

   Método de autenticación basada en sesiones en Django:

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr">What are web sessions? <br><br>Any data exchange on the web is based on a stateless protocol like HTTP. <br><br>Every HTTP request is independent of the previous ones. <br><br>However, users need to relate the requests to each other. <br><br>For example, they want to stay logged in to a website… <a href="https://t.co/6yYQSGv2MP">pic.twitter.com/6yYQSGv2MP</a></p>&mdash; Fernando 🇮🇹🇨🇭 (@Franc0Fernand0) <a href="https://twitter.com/Franc0Fernand0/status/1949031696768070104?ref_src=twsrc%5Etfw">July 26, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

   Otros métodos de autenticación

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Authentication in REST APIs acts as the crucial gateway, ensuring that solely authorized users or applications gain access to the API&#39;s resources.<br><br>Some popular authentication methods for REST APIs include:<br><br>1. Basic Authentication: <br>Involves sending a username and password with… <a href="https://t.co/Y4CKqZUhBF">pic.twitter.com/Y4CKqZUhBF</a></p>&mdash; Alex Xu (@alexxubyte) <a href="https://twitter.com/alexxubyte/status/1737151765097951544?ref_src=twsrc%5Etfw">December 19, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>