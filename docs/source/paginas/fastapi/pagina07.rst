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

Get
^^^

1. Modifique el endpoint `/tasks/` para que solo devuelva las tareas del usuario autenticado, utilizando el token JWT obtenido en el paso anterior.

   .. code-block:: python
      
      import os
      from fastapi import FastAPI, Depends, HTTPException, status
      from fastapi.security import HTTPBearer, HTTPAuthorizationCredentials
      from supabase import create_client, Client

      security = HTTPBearer()

      ... 

      def get_supabase_client(credentials: HTTPAuthorizationCredentials = Depends(security)) -> Client:
         token = credentials.credentials
         try:
            client = create_client(os.getenv("SUPABASE_URL"), os.getenv("SUPABASE_PUBLISHABLE_KEY"))
            client.postgrest.auth(token)
            return client
         except Exception:
            raise HTTPException(
                  status_code=status.HTTP_401_UNAUTHORIZED, 
                  detail="Token de Supabase inválido o expirado"
            )

      @app.get("/tasks/", status_code=status.HTTP_200_OK)
      def get_tasks(supabase: Client = Depends(get_supabase_client)):
         try:
            response = supabase.table("task").select("*").execute()
            
            return response.data

         except Exception as e:
            raise HTTPException(
                  status_code=status.HTTP_500_INTERNAL_SERVER_ERROR,
                  detail="Error al recuperar las tareas desde la base de datos."
            )

2. Entra a `/docs` de tu API y haz clic en el botón candado **Authorize** (ubicado en la esquina superior derecha o al lado del endpoint).
3. En el campo de texto llamado Value, pega directamente el token que obtuviste en el paso anterior y haz clic en el botón **Authorize** y luego cierra el cuadro de diálogo (Close).
4. En `/docs` de tu API, prueba el endpoint `/tasks/` y verifica que solo se devuelvan las tareas asociadas al usuario autenticado.
5. Utiliza un cliente de IAG para explicar la importancia de la autenticación en la API RESTful y cómo el uso de tokens JWT permite a los usuarios acceder únicamente a sus propios datos, mejorando la seguridad y la privacidad de la aplicación.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Cuál es la importancia de la autenticación en una API RESTful y cómo se implementa en FastAPI con Supabase?

    * ¿Cómo se asegura que los usuarios solo puedan acceder a sus propias tareas en la base de datos y en la API?

    * ¿Qué ventajas ofrece el uso de tokens JWT para la autenticación y autorización en aplicaciones web modernas?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Ever wondered how an API knows it&#39;s you, without hitting a database every time?<br>That&#39;s JWT. One signed token, zero lookups.<br>Broke down how it actually works, the alg:none exploit, and the storage tradeoffs nobody warns you about 🧵👇<a href="https://t.co/3HjVSbD4kc">https://t.co/3HjVSbD4kc</a><a href="https://x.com/hashtag/JWT?src=hash&amp;ref_src=twsrc%5Etfw">#JWT</a> <a href="https://x.com/hashtag/API?src=hash&amp;ref_src=twsrc%5Etfw">#API</a> <a href="https://x.com/hashtag/Security?src=hash&amp;ref_src=twsrc%5Etfw">#Security</a> <a href="https://t.co/BMDXR6xzMi">pic.twitter.com/BMDXR6xzMi</a></p>&mdash; Anshul (@TweetYAnshul) <a href="https://x.com/TweetYAnshul/status/2076332305120157699?ref_src=twsrc%5Etfw">July 12, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>