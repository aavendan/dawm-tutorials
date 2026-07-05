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


Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *api*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Conclusiones
============

.. topic:: Preguntas de cierre

    * Compare el uso de parámetros de consulta (Query), parámetros de ruta (Path) y datos enviados en el cuerpo de la solicitud (Body). ¿Qué criterios utilizaría para decidir cuál emplear en una API REST?

    * Justifique si una API debería eliminar permanentemente un recurso o implementar un mecanismo de eliminación lógica (soft delete). Fundamente su respuesta considerando aspectos de seguridad, auditoría y recuperación de información.

    * Proponga una estrategia para registrar un historial de eliminaciones en una API. Explique qué información almacenaría (usuario, fecha, recurso eliminado, motivo, entre otros) y cómo este registro facilitaría las tareas de auditoría.

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">HTTP has introduced a new method: QUERY. <br><br>✅ Safe and idempotent like GET<br>✅ Cacheable by default with BODY <br>✅ Supports request bodies like POST<br>✅ Provides better semantics for search and filtering APIs<br><br>For Fastify users, native app.addHttpMethod(&#39;QUERY&#39;, { hasBody: true });</p>&mdash; Vishnuraj Rajagopal (@vishnuraj910) <a href="https://x.com/vishnuraj910/status/2073674188813177102?ref_src=twsrc%5Etfw">July 5, 2026</a></blockquote> <script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
