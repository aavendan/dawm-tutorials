..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=======================================
Fast API - Despliegue con FastAPI Cloud
=======================================

.. topic:: Objetivo específico
    :class: objetivo

    Desplegar un API RESTful desarrollado con Fast API en la nube utilizando FastAPI Cloud, para permitir el acceso remoto y la comunicación entre el cliente y el servidor mediante el protocolo HTTP.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *api* en Codespaces o en su máquina local.

Actividades en clases
=====================

Módulos requeridos
------------------

1. Instale el módulo *Pipreqs* ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      pip install pipreqs


2. Cree un archivo *requirements.txt* ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      pipreqs . --force --ignore .venv

3. Modifique el archivo *requirements.txt* con la versión estable de Fast API:

   .. code-block:: text

      fastapi[standard]==<VERSION_ESTABLE_DE_FASTAPI>

   **Nota:** Copie la `<VERSION_ESTABLE_DE_FASTAPI>` que aparece disponible.

4. Consulte con un cliente de IAG acerca del contenido del archivo *requirements.txt* con la ejecución de su API.

Punto de partida (entrypoint)
-----------------------------

1. En la raíz de su proyecto, cree un archivo llamado *pyproject.toml* y agregue el siguiente contenido:

   .. code-block:: text

      [project]
      name = "main"
      version = "0.1.0"
      requires-python = ">=3.12"
      dependencies = [
         "fastapi[standard]==<VERSION_ESTABLE_DE_FASTAPI>"
      ]

      [tool.fastapi]
      entrypoint = "main:app"

   
   **Nota:** Reemplace `<VERSION_ESTABLE_DE_FASTAPI>` con la versión estable de Fast API que desea utilizar.
   
   Considerando que la estructura del proyecto es la siguiente:

   .. code-block:: text
    
       api/
        ├── main.py
        ├── pyproject.toml
        └── .gitignore

2. Consulte con un cliente de IAG acerca de la función del archivo *pyproject.toml* y su relación con el despliegue de la API en FastAPI Cloud.

Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *api*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Fast API Cloud
------------------

.. sidebar:: 

   `FastAPI Cloud <https://fastapicloud.com/>`_ está construido por el mismo autor y equipo detrás de FastAPI.

   Agiliza el proceso de construir, desplegar y acceder a una API con el mínimo esfuerzo.

1. Acceda a la página de `FastAPI Cloud <https://fastapicloud.com/>`_ y cree una cuenta gratuita mediante su cuenta de GitHub.
2. Conecte su cuenta de GitHub con Fast API Cloud y seleccione el repositorio de su proyecto *api*.
3. Haga clic en el botón *Deploy* para desplegar su API en la nube.
4. Una vez desplegada, obtenga la URL de su API y verifique que esté funcionando correctamente.

Conclusiones
============

.. topic:: Preguntas de cierre

    * Examine el proceso de validación que realiza FastAPI antes de ejecutar un endpoint de actualización. ¿Cómo contribuye este proceso a reducir errores y mejorar la confiabilidad de la aplicación?

    * ¿Cuáles son las ventajas de utilizar FastAPI Cloud para desplegar una API en comparación con otros servicios de despliegue en la nube? Considere aspectos como facilidad de uso, integración con GitHub y escalabilidad.
    
    * ¿Qué consideraciones de seguridad y privacidad se deben tener en cuenta al desplegar una API en la nube utilizando FastAPI Cloud? ¿Cómo puede proteger los datos sensibles y garantizar el acceso seguro a la API?


Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">FastAPI Cloud is now in Public Beta ⚡<br><br>Deploy <a href="https://x.com/FastAPI?ref_src=twsrc%5Etfw">@FastAPI</a> apps with:<br><br>fastapi deploy<br><br>No waitlist. Try it now. 🚀<br><br>You Code. We Cloud. 😎<a href="https://t.co/HWeZyWbIiP">https://t.co/HWeZyWbIiP</a> <a href="https://t.co/V9OWV5cFHO">pic.twitter.com/V9OWV5cFHO</a></p>&mdash; FastAPI Cloud (@FastAPIcloud) <a href="https://x.com/FastAPIcloud/status/2069171493288755587?ref_src=twsrc%5Etfw">June 22, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>