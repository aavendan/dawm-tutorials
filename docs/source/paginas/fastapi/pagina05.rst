..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=======================================
Fast API - Datos de formulario y estados de respuesta
=======================================

.. topic:: Objetivo específico
    :class: objetivo

    Implementar un API RESTful utilizando Fast API, que permita la comunicación entre el cliente y el servidor, utilizando el protocolo HTTP, con datos de formulario y estados de respuesta.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *api* en Codespaces o en su máquina local.
2. Acceda al ambiente virtual de desarrollo, de acuerdo con su sistema operativo.
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

2. Importe la clase *Form* *Annotated* en el archivo *main.py* y agregue la función *create_item* para que reciba los parámetros *item_name*, *description*, *price* y *tax* como datos de formulario, con el siguiente código:

    .. code-block:: python
        :emphasize-lines: 1,2, 6-13
    
        from typing import Annotated
        from fastapi import FastAPI, Form
    
        ...

        @app.post("/items_form/")
        def create_item(
            item_name: Annotated[str, Form()],
            description: Annotated[str, Form()],
            price: Annotated[float, Form()],
            tax: Annotated[float, Form()]
        ):
            return {"item_name": item_name, "description": description, "price": price, "tax": tax}

3. Compruebe el funcionamiento de la función *create_item* con la herramienta *Swagger UI* y la documentación automática de Fast API.
4. Utilice un cliente de IAG para explicar la importancia de la clase *Form* en la recepción de datos de formulario y *Annotated* en la validación de datos.

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

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">HTTP has introduced a new method: QUERY. <br><br>✅ Safe and idempotent like GET<br>✅ Cacheable by default with BODY <br>✅ Supports request bodies like POST<br>✅ Provides better semantics for search and filtering APIs<br><br>For Fastify users, native app.addHttpMethod(&#39;QUERY&#39;, { hasBody: true });</p>&mdash; Vishnuraj Rajagopal (@vishnuraj910) <a href="https://x.com/vishnuraj910/status/2073674188813177102?ref_src=twsrc%5Etfw">July 5, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
