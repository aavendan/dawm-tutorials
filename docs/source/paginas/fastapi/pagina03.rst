..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===================================
Fast API - Despliegue de la API
===================================

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

