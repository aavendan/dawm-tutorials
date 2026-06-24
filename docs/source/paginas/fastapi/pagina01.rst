..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===================================
Fast API - Introducción
===================================

.. topic:: Objetivo específico
    :class: objetivo

    Utilizar Fast API para crear un API RESTful, que permita la comunicación entre el cliente y el servidor, utilizando el protocolo HTTP.


Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Cree un repositorio en GitHub con el nombre *api*.

   a) Agregue un archivo README.md con el título de su API y una breve descripción del objetivo de su proyecto.
   b) Agregue un archivo *.gitignore* con la plantilla de *Python*.
   
2. Acceda a su proyecto *api* en Codespaces o en su máquina local.
3. Cree y utilice la(s) rama(s) de desarrollo.

Actividades en clases
=====================

1. Explore la documentación de `Fast API <https://fastapi.tiangolo.com/>`_ para comprender los conceptos básicos de este framework.
2. Dentro de la carpeta de su proyecto, abra la terminal e instale Fast API y Uvicorn ejecutando el siguiente comando:

   .. code-block:: bash

      pip install "fastapi[standard]"

main.py
--------------

1. Cree un archivo llamado *main.py* en la raíz de su proyecto.
2. Implemente un ejemplo básico de Fast API en el archivo *main.py*:

   .. code-block:: python

      from fastapi import FastAPI

      app = FastAPI()

      @app.get("/")
      def read_root():
          return {"message": "¡Hola, Fast API!"}


Servidor de desarrollo
----------------------

1. Inicie el servidor de desarrollo ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      fastapi dev

2. Abra su navegador web y acceda a `http://127.0.0.1:8000`_ para ver la respuesta de su API.
3. Verifique que la respuesta sea un JSON con el mensaje:

   .. code-block:: json
    
      {
        "message": "¡Hola, Fast API!"
      }

Documentación interactiva de la API
-----------------------------------

1. Acceda a la documentación interactiva de su API en `http://127.0.0.1:8000/docs`_.
2. Explore el endpoint `/` y pruebe la respuesta de su API utilizando la interfaz interactiva.

    a) Haga clic en el botón "Try it out" para habilitar la prueba del endpoint.
    b) Haga clic en el botón "Execute" para enviar la solicitud y ver la respuesta de su API.
    c) Verifique que la respuesta sea un JSON con el mensaje:

       .. code-block:: json
    
          {
            "message": "¡Hola, Fast API!"
          }

3. Explore la documentación alternativa de su API mediante Swagger UI en `https://swagger.io/tools/swagger-ui/`_.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Qué es Fast API y cuáles son sus principales características?

    * ¿Cómo se instala Fast API y Uvicorn en un proyecto de Python?

    * ¿Cómo se crea un archivo *main.py* y se implementa un ejemplo básico de Fast API?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">There&#39;s now an official <a href="https://x.com/Redisinc?ref_src=twsrc%5Etfw">@Redisinc</a> SDK for FastAPI 🚀 <a href="https://t.co/3j91awnIhX">https://t.co/3j91awnIhX</a></p>&mdash; FastAPI (@FastAPI) <a href="https://x.com/FastAPI/status/2069729232922480959?ref_src=twsrc%5Etfw">June 24, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>