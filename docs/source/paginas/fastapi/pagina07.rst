..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

=================================
Fast API - Seguridad
=================================

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

Modificar la base de datos
^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Ejecuta el siguiente script en el SQL Editor de tu consola de Supabase para modificar la tabla `task`, de tal forma que contenga una columna para identificar al dueño de la tarea (usualmente enlazada a la tabla auth.users de Supabase) y active las políticas de seguridad.

   .. code-block:: sql

      ALTER TABLE task ADD COLUMN IF NOT EXISTS user_id UUID REFERENCES auth.users(id) DEFAULT auth.uid();

      ALTER TABLE task ENABLE ROW LEVEL SECURITY;

      CREATE POLICY "Usuarios pueden leer sus propias tareas" 
      ON task 
      FOR SELECT 
      TO authenticated 
      USING (auth.uid() = user_id);

      CREATE POLICY "Usuarios pueden crear sus propias tareas" 
      ON task 
      FOR INSERT 
      TO authenticated 
      WITH CHECK (auth.uid() = user_id);

2. Utiliza un cliente IAG para explicar la importancia de las políticas de seguridad en la base de datos y cómo estas ayudan a proteger los datos de los usuarios, asegurando que solo puedan acceder a sus propias tareas.

Usuario
^^^^^^^

1. En Supabase, acceda a la sección *Authentication* y cree un usuario de prueba, con el correo electrónico **test@example.com** y una contraseña segura.
2. Busca al usuario en la lista y copia el valor de la columna User UID (un código largo con guiones, por ejemplo: `a1b2c3d4-e5f6-7a8b-9c0d-1e2f3a4b5c6d`).
3. Actualiza la tabla `task` para asignar el User UID del usuario de prueba a las tareas existentes, ejecutando el siguiente script en el SQL Editor de Supabase:

   .. code-block:: bash

      UPDATE task 
      SET user_id = 'AQUÍ_PEGA_EL_UUID_DEL_USUARIO'
      WHERE user_id IS NULL;

4. Utiliza un cliente de IAG para explicar la importancia de asignar un User UID a las tareas existentes y cómo esto garantiza que cada tarea esté asociada a un usuario específico, mejorando la seguridad y la gestión de los datos en la aplicación.

FastAPI
--------

Autenticación
^^^^^^^^^^^^^

1. Añade la autenticación a tu API RESTful utilizando FastAPI y Supabase, de tal forma que los usuarios solo puedan acceder a sus propias tareas.

   .. code-block:: python
      :emphasize-lines: 1, 5-17

      import requests
      
      ...

      @app.post("/auth/login-temporal")
      def login_temporal(email: str, password: str):
         # Endpoint nativo de Supabase Auth
         url = f"{os.getenv('SUPABASE_URL')}/auth/v1/token?grant_type=password"
         headers = {"apikey": os.getenv("SUPABASE_PUBLISHABLE_KEY"), "Content-Type": "application/json"}
         payload = {"email": email, "password": password}
         
         response = requests.post(url, json=payload, headers=headers)
         if response.status_code != 200:
            raise HTTPException(status_code=400, detail="Credenciales incorrectas en Supabase")
            
         # Retornamos el access_token que es el JWT que necesitas
         return {"access_token": response.json().get("access_token")}

2. En `/docs` de tu API, prueba el endpoint `/auth/login-temporal` con el correo electrónico y la contraseña del usuario de prueba que creaste en Supabase. 



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