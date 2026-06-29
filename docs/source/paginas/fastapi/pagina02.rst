..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===========================================
Fast API - Parámetros de ruta y de consulta
===========================================

.. topic:: Objetivo específico
    :class: objetivo

    Planificar y desarrollar un API RESTful utilizando Fast API, que permita la comunicación entre el cliente y el servidor, utilizando el protocolo HTTP mediante parámetros de ruta y de consulta.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *api* en Codespaces o en su máquina local.
2. Instale las depedencias de su proyecto, con:

   .. code-block:: bash

      pip install .

Actividades en clases
=====================

Ambiente Virtual de Desarrollo
------------------------------

1. Cree un :term:`ambiente virtual de desarrollo` en la raíz de su proyecto, con el nombre *venv*, ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      python -m venv .venv

2. Active el ambiente virtual de desarrollo ejecutando el siguiente comando en la terminal:

   .. tab-set::

      .. tab-item:: Linux / macOS
         
         .. code-block:: bash

            source .venv/bin/activate 
      
      .. tab-item:: Windows
         
         .. code-block:: bash

            source .venv/Scripts/activate

3. Instale los paquetes requeridos ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      pip install .

4. Inicie el servidor de desarrollo ejecutando el siguiente comando en la terminal:

   .. code-block:: bash

      fastapi dev

5. Consulte con un cliente de IAG acerca del ambiente virtual de desarrollo y su importancia en la gestión de dependencias de un proyecto.

Parámetros de ruta
------------------

1. Modifique el archivo *main.py*, con:

   .. code-block:: python
      :emphasize-lines: 6-8

      ...

      def read_root():
          ...

      @app.get("/items/{item_id}")
      def read_item(item_id):
         return {"item_id": item_id}

2. Realice una solicitud GET a la ruta `/items/products` y observe la respuesta del servidor.
3. Consulte con un cliente de IAG acerca de la respuesta del servidor y paso del valor del parámetro de ruta `item_id` como argumento de la función.

Tipo de datos
^^^^^^^^^^^^^

.. sidebar::

   Fast API utiliza `Pydantic <https://pydantic.dev/docs/>`_ para validar y serializar los datos de entrada y salida en las rutas del API.

1. Modifique el archivo *main.py*, con:

   .. code-block:: python
      :emphasize-lines: 7

      ...

      def read_root():
          ...

      @app.get("/items/{item_id}")
      def read_item(item_id: int):
         return {"item_id": item_id}

2. Utilice su navegador web para realizar una solicitud GET a las rutas `/items/1` y `/items/products`. Consulte con un cliente de IAG acerca de cómo el parámetro de ruta `item_id` pasa como argumento de la función usando anotaciones de tipos estándar de Python y sus limitaciones.
3. Inspeccione la documentación interactiva (`http://localhost:8000/docs`) y alternativa (`http://localhost:8000/redoc`) de su API. Consulte con un cliente de IAG acerca de cómo se refleja el tipo de dato del parámetro de ruta `item_id` en la documentación.

Parámetros de consulta
----------------------

1. Modifique el archivo *main.py*, con:

   .. code-block:: python
      :emphasize-lines: 3, 8-11

      ...

      fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}, {"item_name": "Qux"}, {"item_name": "Quux"}, {"item_name": "Corge"}, {"item_name": "Grault"}, {"item_name": "Garply"}, {"item_name": "Waldo"}, {"item_name": "Fred"}, {"item_name": "Plugh"}, {"item_name": "Xyzzy"}, {"item_name": "Thud"}]

      def read_root():
          ...

      @app.get("/items/")
      def read_item(skip: int = 0, limit: int = 10):
         results = fake_items_db[skip : skip + limit]
         return results

2. Realice una solicitud GET a la ruta `/items/?skip=0&limit=10` y observe la respuesta del servidor.
3. Consulte con un cliente de IAG acerca de la respuesta del servidor y el valor de los parámetros de consulta `skip` y `limit`.

Parámetros opcionales
^^^^^^^^^^^^^^^^^^^^^

1. Modifique el archivo *main.py*, con:

   .. code-block:: python
      :emphasize-lines: 9-13

      ...

      fake_items_db = [ ... ]

      def read_root():
          ...

      @app.get("/items/")
      def read_item(skip: int = 0, limit: int = 10, q: str | None = None):
         results = fake_items_db[skip : skip + limit]
         if q:
            results.append({"item_name": q})
         return results

2. Consulte con un cliente de IAG acerca de la respuesta del servidor y el valor del parámetro de consulta opcional `q`.


Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *api*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Conclusiones
============

.. topic:: Preguntas de cierre

    * Evalúe la importancia de la validación automática de datos antes de ejecutar la lógica de negocio de un endpoint. ¿Qué riesgos podrían presentarse si esta validación no existiera?

    * Proponga la estructura de una API para gestionar productos de una tienda virtual utilizando los conceptos presentados en el tutorial. Describa los modelos necesarios, los endpoints principales y cómo aprovecharía la validación automática para minimizar errores.

    * Valore el impacto que tendría reutilizar un mismo modelo de datos en múltiples endpoints de una API. ¿Cómo afecta esta decisión la mantenibilidad, consistencia y escalabilidad del proyecto?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr"><a href="https://x.com/hashtag/LSPPDay23?src=hash&amp;ref_src=twsrc%5Etfw">#LSPPDay23</a><br><br>🔗 Built a mini URL Shortener API with FastAPI today. Learned how route parameters work and how backend applications map short codes to actual URLs through API endpoints.<a href="https://x.com/lftechnology?ref_src=twsrc%5Etfw">@lftechnology</a><a href="https://x.com/hashtag/60DaysOfLearning2026?src=hash&amp;ref_src=twsrc%5Etfw">#60DaysOfLearning2026</a> <a href="https://x.com/hashtag/LearningWithLeapfrog?src=hash&amp;ref_src=twsrc%5Etfw">#LearningWithLeapfrog</a> <a href="https://t.co/LUIKcdiGsA">pic.twitter.com/LUIKcdiGsA</a></p>&mdash; Preeyanka Khatri Xettri (@preeyanka07) <a href="https://x.com/preeyanka07/status/2070194299627790747?ref_src=twsrc%5Etfw">June 25, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>