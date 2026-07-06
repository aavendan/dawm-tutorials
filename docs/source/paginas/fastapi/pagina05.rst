..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=====================================================
Fast API - Datos de formulario y estados de respuesta
=====================================================

.. topic:: Objetivo específico
    :class: objetivo

    Implementar un API RESTful utilizando Fast API, que permita la comunicación entre el cliente y el servidor, utilizando el protocolo HTTP, con datos de formulario y estados de respuesta.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *api* en Codespaces o en su máquina local.
2. Acceda al ambiente virtual de desarrollo, de acuerdo con su sistema operativo.

   .. code-block:: bash

      python -m venv .venv

      # Para Linux / macOS
      source .venv/bin/activate
    
      # Para Windows
      .venv/Scripts/activate

3. Instale las dependencias del proyecto, con:

   .. code-block:: bash

      python -m pip install -r requirements.txt

4. Levante el servidor, con:

   .. code-block:: bash

      fastapi dev

Actividades en clases
=====================

Python-Multipart
----------------

1. En la línea de comando de su proyecto *api*, ejecute el siguiente comando para instalar la dependencia *python-multipart*:

   .. code-block:: bash

      python -m pip install python-multipart

2. Utilice un cliente de IAG para explicar la importancia de la dependencia *python-multipart* en la recepción de datos de formulario.

Datos de formulario
-------------------

1. Modifique el archivo *main.py*, con:

   a) Importe la clase *Form* de la librería *fastapi* y la clase *Annotated* de la librería *typing*
   b) Agregue la función *create_item* para que reciba los parámetros *item_name*, *description*, *price* y *tax* como datos de formulario

   .. code-block:: python
      :emphasize-lines: 1,2, 6-12, 14

      from fastapi import FastAPI, Form
      from typing import Annotated
      
      ...

      @app.post("/items_form/")
      def create_item(
        item_name: Annotated[str, Form()],
        description: Annotated[str, Form()],
        price: Annotated[float, Form()],
        tax: Annotated[float, Form()]
      ):

        return {"item_name": item_name, "description": description, "price": price, "tax": tax}

2. Compruebe el funcionamiento de la función *create_item* con la herramienta *Swagger UI* y la documentación automática de Fast API. 
3. Analice la diferencia entre la función *create_item* que recibe un objeto de tipo *Item* y la función *create_item* que recibe los parámetros como datos de formulario.

Modelo de formulario de datos
-----------------------------

1. Cree una clase llamada *FormData* que herede de la clase *BaseModel* en el archivo *models/form_data.py*, con los siguientes atributos:

   .. code-block:: python
      :emphasize-lines: 1, 3-7

      from pydantic import BaseModel

      class FormData(BaseModel):
        item_name: str
        description: str
        price: float
        tax: float

2. Modifique la función *create_item* para que reciba un objeto de tipo *FormData* como parámetro, en lugar de los parámetros individuales.

   .. code-block:: python
      :emphasize-lines: 2, 14-19, 21, 23
    
      from fastapi import FastAPI, Form
      from models.form_data import FormData
    
      ...

      @app.post("/items_form/")
      def create_item(
        item_name: Annotated[str, Form()],
        description: Annotated[str, Form()],
        price: Annotated[float, Form()],
        tax: Annotated[float, Form()]
      ):

        form_data = FormData(
            item_name=item_name,
            description=description,
            price=price,
            tax=tax
        )

        message = f"Item '{form_data.item_name}' created successfully with description '{form_data.description}', price {form_data.price}, and tax {form_data.tax}." 

        return message

Estados de respuesta
---------------------

201 Created
^^^^^^^^^^^

1. Modifique el archivo *main.py*, con:

   a) Importe la clase `Response <https://fastapi.tiangolo.com/reference/response/>`_ de la librería *fastapi*
   b) Agregue la función *create_item* para que retorne un estado de respuesta 201 (Created) y un mensaje de éxito

   .. code-block:: python
      :emphasize-lines: 1, 16, 18
    
      from fastapi import FastAPI, Form, Response
    
      ...

      @app.post("/items_form/")
      def create_item(
        item_name: Annotated[str, Form()],
        description: Annotated[str, Form()],
        price: Annotated[float, Form()],
        tax: Annotated[float, Form()]
      ):
            ...

        message = f"Item '{form_data.item_name}' created successfully with description '{form_data.description}', price {form_data.price}, and tax {form_data.tax}." 

        fake_items_db.append(item_name)

        return Response(content=message, status_code=201)

2. Compruebe el funcionamiento de la función *create_item* con la herramienta *Swagger UI* y la documentación automática de Fast API.

Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *api*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Cuál es la diferencia entre recibir un objeto de tipo *Item* y recibir los parámetros como datos de formulario en una función de Fast API?

    * ¿Cuál es la importancia de la dependencia *python-multipart* en la recepción de datos de formulario en Fast API?

    * ¿Cuál es la diferencia entre retornar un estado de respuesta 200 (OK) y un estado de respuesta 201 (Created) en una función de Fast API?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">HTTP has introduced a new method: QUERY. <br><br>✅ Safe and idempotent like GET<br>✅ Cacheable by default with BODY <br>✅ Supports request bodies like POST<br>✅ Provides better semantics for search and filtering APIs<br><br>For Fastify users, native app.addHttpMethod(&#39;QUERY&#39;, { hasBody: true });</p>&mdash; Vishnuraj Rajagopal (@vishnuraj910) <a href="https://x.com/vishnuraj910/status/2073674188813177102?ref_src=twsrc%5Etfw">July 5, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
