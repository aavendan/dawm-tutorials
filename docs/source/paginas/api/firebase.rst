..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

==========================================
Guía 10: Firebase: Realtime Database y SDK
==========================================

.. topic:: Objetivo específico
    :class: objetivo

    Integrar Firebase Realtime Database utilizando su SDK para el almacenamiento y recuperación de datos en tiempo real permitiendo una experiencia de usuario dinámica e interactiva.

Actividades previas
=====================

Firebase: Proyecto
------------------

1. Acceda a `Firebase <https://firebase.google.com/>`_ con su cuenta personal de Google.
2. En `Firebase Console <https://console.firebase.google.com/>`_, cree el proyecto **landing**. No es necesario configurar Google Analytics para este proyecto.
3. Utilice un cliente de IAG para explicar los servicios, y sus casos prácticos de uso, que ofrece Firebase.

Actividades en clases
=====================

Firebase: App - web
-------------------

1. En su proyecto de Firebase:
   
   a) Junto a **Project Overview**, despliegue el menú de configuración del proyecto y escoja **Project settings**.
   b) En la pestaña **General**, desplácese hasta la sección **Your apps**.
   c) Haga clic en el ícono de elemento HTML para crear una **web app**.

Realtime Database
^^^^^^^^^^^^^^^^^

1. Dentro de su proyecto en Firebase, acceda a la categoría de productos **Build**, en la opción **Realtime Database**.
2. Cree una base de datos en tiempo real seleccionando **Create Database**.
   
   a) Seleccione la ubicación de la base de datos, preferiblemente la más cercana a su usuario final.
   b) En **Security rules**, elija **Start in Test Mode** para permitir el acceso sin restricciones durante el desarrollo inicial. 
   
   .. attention:: 

      **Nota de seguridad**: El modo de prueba permite que cualquier persona pueda leer y escribir en la base de datos sin autenticación. 
      Esto es útil para pruebas, pero asegúrese de cambiar a un modo más seguro antes de desplegar su aplicación en producción.

3. Utilice una cliente de IAG para explicar cómo se estructura la base de datos en tiempo real de Firebase.

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Qué desafíos conceptuales encontraste al interpretar el código generado por IA para integrar Firebase en tu landing page?

    * ¿Qué modificaciones realizaste al código sugerido por la IA para adaptarlo a los requerimientos específicos de tu landing page?

    * ¿Cómo aseguras que el uso de IA en la implementación de Firebase no sustituya tu comprensión del flujo de datos ni tu responsabilidad en el manejo seguro de la información del usuario?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="es" dir="ltr">🔥 <a href="https://twitter.com/hashtag/Firebase?src=hash&amp;ref_src=twsrc%5Etfw">#Firebase</a> está preparando un nuevo SDK para JavaScript que hará la librería más ligera y traerá cambios importantes que nos harán refactorizar nuestras apps si queremos aprovechas sus ventajas.<br><br>🧵 Te las cuento en el hilo 👇 <a href="https://t.co/oJHLopDw1J">pic.twitter.com/oJHLopDw1J</a></p>&mdash; Carlos Azaustre 💻 (@carlosazaustre) <a href="https://twitter.com/carlosazaustre/status/1421036271242252288?ref_src=twsrc%5Etfw">July 30, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>