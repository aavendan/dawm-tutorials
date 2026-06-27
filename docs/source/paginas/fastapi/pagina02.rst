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

2. Realice una solicitud GET a la ruta `http://127.0.0.1:8000/items/products` y observe la respuesta del servidor.
3. Consulte con un cliente de IAG acerca de la respuesta del servidor y el valor del parámetro de ruta `item_id`.

Parámetros de consulta
----------------------

1. Modifique el archivo *main.py*, con:

   .. code-block:: python
      :emphasize-lines: 6-8

      ...

      def read_root():
          ...

      @app.get("/items/{item_id}")
      def read_item(item_id, q: str = None):
         return {"item_id": item_id, "q": q}

2. Realice una solicitud GET a la ruta `http://127.0.0.1:8000/items/products?q=example` y observe la respuesta del servidor.
3. Consulte con un cliente de IAG acerca de la respuesta del servidor y el valor del parámetro de consulta `q`.

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

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr"><a href="https://x.com/hashtag/LSPPDay23?src=hash&amp;ref_src=twsrc%5Etfw">#LSPPDay23</a><br><br>🔗 Built a mini URL Shortener API with FastAPI today. Learned how route parameters work and how backend applications map short codes to actual URLs through API endpoints.<a href="https://x.com/lftechnology?ref_src=twsrc%5Etfw">@lftechnology</a><a href="https://x.com/hashtag/60DaysOfLearning2026?src=hash&amp;ref_src=twsrc%5Etfw">#60DaysOfLearning2026</a> <a href="https://x.com/hashtag/LearningWithLeapfrog?src=hash&amp;ref_src=twsrc%5Etfw">#LearningWithLeapfrog</a> <a href="https://t.co/LUIKcdiGsA">pic.twitter.com/LUIKcdiGsA</a></p>&mdash; Preeyanka Khatri Xettri (@preeyanka07) <a href="https://x.com/preeyanka07/status/2070194299627790747?ref_src=twsrc%5Etfw">June 25, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>