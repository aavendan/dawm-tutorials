..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=====================================================
Fast API - Supabase y testing de API RESTful
=====================================================

.. topic:: Objetivo específico
    :class: objetivo

    Implementar un API RESTful utilizando Fast API, que permita la comunicación entre el cliente y el servidor, utilizando el protocolo HTTP, con Supabase como base de datos y testing de la API.

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

Supabase
--------

1. Crea una cuenta en `Supabase <https://supabase.com/>`_ y cree un proyecto.
2. En la pantalla inicial del proyecto, obtenga las variables de entorno necesarias para conectarse a la base de datos:

   a) En el botón *Copy*, acceda a la opción *Get Connected*
   b) Escoja la pestaña *Server / Build APIs* y copie la variables de entorno **SUPABASE_URL** y **SUPABASE_PUBLISHABLE_KEY**, que servirán para conectarse FastAPI con Supabase.

3. Utilice un cliente de IAG para explicar la importancia de la base de datos Supabase en una API RESTful y cómo se puede utilizar para almacenar y recuperar datos de manera eficiente.

Tabla: Item
^^^^^^^^^^^

1. En el panel lateral, acceda a la opción *SQL Editor* y cree una tabla llamada *Task* con los siguientes campos:

   - id: integer, primary key, auto increment
   - title: text, not null
   - description: text, nullable
   - created_at: timestamp, default current_timestamp

   .. code-block:: sql

      CREATE TABLE task (
        id SERIAL PRIMARY KEY,
        title VARCHAR(255) NOT NULL,
        description TEXT,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
      );

2. Ejecute la consulta SQL para crear la tabla **Run and enable RLS**. 
3. Verifique que se haya creado correctamente en la base de datos en el panel lateral, en *Database* > *Schema Visualizer*.
4. Utilice un cliente de IAG para explicar la importancia de *Run and enable RLS* en la tabla *Task* y cómo se puede utilizar para controlar el acceso a los datos de manera segura.

FastAPI 
-------

Configuración
^^^^^^^^^^^^^

1. En la raíz del proyecto *api*, cree el archivo `.env` y agregue las variables de entorno **SUPABASE_URL** y **SUPABASE_PUBLISHABLE_KEY** con los valores obtenidos en el paso 2 de la sección *Supabase*.

   .. code-block:: bash

      SUPABASE_URL=<su_supabase_url>
      SUPABASE_PUBLISHABLE_KEY=<su_supabase_publishable_key>

2. Instale la dependencia *supabase* en el ambiente virtual de desarrollo, con:

   .. code-block:: bash

      python -m pip install supabase

3. Utilice un cliente de IAG para explicar la importancia de la dependencia *supabase* en la conexión de FastAPI con la base de datos Supabase y cómo se puede utilizar para realizar operaciones CRUD en la tabla *Task*.
 
Modelo de datos
^^^^^^^^^^^^^^^

1. Cree el archivo *models/task.py* y cree una clase llamada *Task* que herede de la clase *BaseModel*, con los siguientes atributos:

   .. code-block:: python
      :emphasize-lines: 1, 3-6

      from pydantic import BaseModel

      class Task(BaseModel):
         id: int | None = None
         title: str
         description: str | None = None
         created_at: str | None = None

2. Modifique el archivo *main.py* para importar la clase *Task* y agregue las funciones *create_task*, *get_tasks*, *get_task*, *update_task* y *delete_task* para realizar operaciones CRUD en la tabla *Task* de la base de datos Supabase.

   .. code-block:: python
      
      ...

      from models.task import Task
      from supabase import create_client, Client
      from dotenv import load_dotenv

      load_dotenv()
      supabase: Client = create_client(os.getenv("SUPABASE_URL"), os.getenv("SUPABASE_KEY"))

      @app.post("/tasks/")
      def create_task(task: Task):
        data = supabase.table("tasks").insert({
            "title": task.title,
            "description": task.description
        }).execute()
        return data.data

      @app.get("/tasks/")
      def get_tasks():
         data = supabase.table("tasks").select("*").execute()
         return data.data

3. Utilice un cliente de IAG para explicar la importancia de la clase *Task* en la validación de datos y cómo se puede utilizar para representar los datos de la tabla *Task* en la API RESTful.

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

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Day 21 building <a href="https://t.co/nGeowdmXnb">https://t.co/nGeowdmXnb</a> 🚀<br><br>Set up backend infrastructure today:<br><br>– <a href="https://x.com/FastAPI?ref_src=twsrc%5Etfw">@FastAPI</a> backend <br>– <a href="https://x.com/supabase?ref_src=twsrc%5Etfw">@supabase</a> for database <br>– <a href="https://x.com/Cloudflare?ref_src=twsrc%5Etfw">@Cloudflare</a> R2 for file storage <br><br>Been using this stack for a long time and still really happy with the balance of simplicity and power.<br><br>Also…</p>&mdash; Alex Kharlamov (@alex_kharlamov_) <a href="https://x.com/alex_kharlamov_/status/2051775076199014722?ref_src=twsrc%5Etfw">May 5, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>