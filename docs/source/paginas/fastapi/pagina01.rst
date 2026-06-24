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

2. Abra su navegador web y acceda a `http://127.0.0.1:8000` para ver la respuesta de su API.
3. Verifique que la respuesta sea un JSON con el mensaje:

   .. code-block:: json
    
      {
        "message": "¡Hola, Fast API!"
      }

Documentación interactiva de la API
-----------------------------------

1. Acceda a la documentación interactiva de su API en `http://127.0.0.1:8000/docs`.
2. Explore el endpoint `/` y pruebe la respuesta de su API utilizando la interfaz interactiva.

   a) Haga clic en el botón "Try it out" para habilitar la prueba del endpoint.
   b) Haga clic en el botón "Execute" para enviar la solicitud y ver la respuesta de su API.
   c) Verifique que la respuesta sea un JSON con el mensaje:

      .. code-block:: json
    
         {
            "message": "¡Hola, Fast API!"
         }

3. Explore la documentación alternativa de su API mediante `Swagger <https://swagger.io/tools/swagger-ui/>`_.

Documentación alternativa de la API
-----------------------------------

.. sidebar:: 

   FastAPI genera un definición o descripción con toda tu API utilizando el estándar `OpenAPI <https://github.com/OAI/OpenAPI-Specification>`_ para definir APIs.

1. Acceda a la documentación alternativa  de su API en `http://127.0.0.1:8000/redoc`.
2. Explore el endpoint `/` y pruebe la respuesta de su API utilizando la interfaz.
3. Descargue la documentación de su API en formato JSON desde la opción **"Download OpenAPI specification"**, en la parte superior de la página.
4. Analice el archivo JSON descargado para comprender la estructura de la documentación generada por FastAPI.

   .. code-block:: json

      {
        "openapi": "3.1.0",
        "info": {
            "title": "FastAPI",
            "version": "0.1.0"
        },
        "paths": {
            "/items/": {
                "get": {
                    "responses": {
                        "200": {
                            "description": "Successful Response",
                            "content": {
                                "application/json": {



      ...

5. Revise la documentación alternativa de su API mediante `ReDoc <https://redocly.github.io/redoc/>`_.

Despliegue de la API
----------------------

1. Obtenga una cuenta en `FastAPI Cloud <https://fastapicloud.com/>`_ mediante su cuenta en GitHub.
2. Seleccione su proyecto **api** y siga las instrucciones de despliegue.
3. Verifique que su API esté funcionando correctamente en la URL proporcionada por FastAPI Cloud.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Qué tipo de tareas relacionadas con el desarrollo de una API en FastAPI podrían ser asistidas por una herramienta de inteligencia artificial generativa y cuáles deberían seguir siendo responsabilidad del desarrollador?

    * ¿Cómo podría utilizarse una IA generativa para detectar errores, redundancias o inconsistencias en una API desarrollada con FastAPI?

    * ¿En qué medida el uso de IA generativa modifica las competencias que debe desarrollar un ingeniero de software al construir APIs?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">There&#39;s now an official <a href="https://x.com/Redisinc?ref_src=twsrc%5Etfw">@Redisinc</a> SDK for FastAPI 🚀 <a href="https://t.co/3j91awnIhX">https://t.co/3j91awnIhX</a></p>&mdash; FastAPI (@FastAPI) <a href="https://x.com/FastAPI/status/2069729232922480959?ref_src=twsrc%5Etfw">June 24, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>