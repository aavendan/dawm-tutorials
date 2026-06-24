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