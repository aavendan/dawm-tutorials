..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=======================================
Fast API - Cuerpo de la solicitud y respuestas personalizadas
=======================================

.. topic:: Objetivo específico
    :class: objetivo

    Implementar un API RESTful utilizando Fast API, que permita la comunicación entre el cliente y el servidor, utilizando el protocolo HTTP, con manejo de errores y respuestas personalizadas.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *api* en Codespaces o en su máquina local.
2. Acceda al ambiente virtual de desarrollo, de acuerdo con su sistema operativo.
3. Instale los paquetes y levante el servidor, con:

   .. code-block:: bash

      fastapi dev

Actividades en clases
=====================

BaseModel de Pydantic
---------------------

1. Cree una clase llamada *Item* que herede de la clase *BaseModel* en el archivo *models/item.py*, con los siguientes atributos:

   .. code-block:: python

      class Item(BaseModel):
         item_name: str
         description: str | None = None
         price: float | None = None
         tax: float | None = None

2. Importe la clase *Item* en el archivo *main.py* y agregue la función *create_item* para que reciba un objeto de tipo *Item* como parámetro, con el siguiente código:

   .. code-block:: python
      :emphasize-lines: 2, 6-8

      from fastapi import FastAPI
      from models.item import Item

      ...

      @app.post("/items/")
      def create_item(item: Item):
         return item


Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *api*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Conclusiones
============

.. topic:: Preguntas de cierre

    * 

    *

    *

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr">HTTP and Rest are not the same things 😋<br><br>🟢HyperText Transfer Protocol is an application layer protocol that defines how clients and servers communicate over the web. It specifies the structure of requests and responses, including HTTP methods (GET, POST, PUT, PATCH, DELETE),…</p>&mdash; vin (@tinivvinit) <a href="https://x.com/tinivvinit/status/2070829550234140742?ref_src=twsrc%5Etfw">June 27, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>