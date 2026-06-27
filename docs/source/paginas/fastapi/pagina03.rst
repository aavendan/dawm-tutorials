..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===================================
Fast API - Despliegue de la API
===================================

.. topic:: Objetivo específico
    :class: objetivo

    Utilizar Fast API para crear un API RESTful, que permita la comunicación entre el cliente y el servidor, utilizando el protocolo HTTP.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *api* en Codespaces o en su máquina local.

Actividades en clases
=====================

Punto de partida (entrypoint)
-----------------------------

1. En la raíz de su proyecto, cree un archivo llamado *pyproject.toml* y agregue el siguiente contenido:

   .. code-block:: text

      [tool.fastapi]
      entrypoint = "main:app"

   Considerando que la estructura del proyecto es la siguiente:

   .. code-block:: text
    
       api/
        ├── main.py
        ├── pyproject.toml
        └── .gitignore

Módulos requeridos
------------------

1. Instale el módulo *Pipreqs* ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      pip install pipreqs


2. Cree un archivo *requirements.txt* ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      pipreqs . --force --ignore .venv

3. Consulte con un cliente de IAG acerca del contenido del archivo *requirements.txt* para verificar que contenga las dependencias necesarias para ejecutar su API.

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

    * ¿Cuál es la URL de su API desplegada en FastAPI Cloud?

    * ¿Cuál es la diferencia entre ejecutar su API en un servidor local y desplegarla en la nube?
    
    * ¿Qué ventajas ofrece el despliegue en la nube para su API en comparación con un servidor local?


Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">FastAPI Cloud is now in Public Beta ⚡<br><br>Deploy <a href="https://x.com/FastAPI?ref_src=twsrc%5Etfw">@FastAPI</a> apps with:<br><br>fastapi deploy<br><br>No waitlist. Try it now. 🚀<br><br>You Code. We Cloud. 😎<a href="https://t.co/HWeZyWbIiP">https://t.co/HWeZyWbIiP</a> <a href="https://t.co/V9OWV5cFHO">pic.twitter.com/V9OWV5cFHO</a></p>&mdash; FastAPI Cloud (@FastAPIcloud) <a href="https://x.com/FastAPIcloud/status/2069171493288755587?ref_src=twsrc%5Etfw">June 22, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>