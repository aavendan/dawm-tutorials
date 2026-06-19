..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===================================
React
===================================

.. topic:: Objetivo específico
    :class: objetivo

    Utilizar React para construir la estructura inicial del dashboard para mejorar la usabilidad e interfaz del sistema.
 

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su repositorio *dashboard* en GitHub 
2. Acceda al Codespaces de su proyecto.

Actividades en clases
=====================

React: Inicialización del proyecto
----------------------------------

.. sidebar:: 

   React implementa la técnica web de desarrollo :term:`Client Side Rendering (CSR)` donde el navegador carga archivos JavaScript, renderiza la página en el lado del cliente y envía un documento HTML completo al navegador para construir interfaces de usuario. 

1. Explore la documentación de `React <https://react.dev/>`_ para comprender los conceptos básicos de esta biblioteca.
2. Cree un proyecto de React utilizando `Vite <https://vitejs.dev/guide/#scaffolding-your-first-vite-project>`_.

   a) Dentro de la carpeta de su proyecto, abra la terminal y cree un nuevo proyecto de Vite con el siguiente comando:

   .. code-block:: bash

      npm create vite@latest . 
   
   b) Preserve los archivos existentes y sobrescriba los archivos de configuración y código fuente del proyecto. 
   c) Seleccione el framework como :term:`React` y la variante como `TypeScript`.
   d) Instale las dependencias del proyecto e inicie el servidor de desarrollo con los siguientes comandos:

   .. code-block:: bash

      npm install
      npm run dev

3. Compruebe la vista previa del resultado en el navegador.

Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *dashboard*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Configuración para el despliegue
--------------------------------

1. Desde la línea de comandos:

   a) Instale el paquete `gh-pages`

   .. code-block:: 

        npm install gh-pages --save-dev
   
2. Modifique el archivo `package.json`, con:

   a) La entrada **homepage**. Reemplace `<username>` por su nombre de usuario.
   b) Los comandos **predeploy** y **deploy** a la entrada **scripts**.

   .. code-block:: 
       :emphasize-lines: 3,7,8

       {
            ...
            "homepage": "https://<username>.github.io/dashboard",
            ...
            "scripts": { 
                ...
                "predeploy": "npm run build",
                "deploy": "gh-pages -d dist",
                ...
            }
       }

3. Modifique el archivo `vite.config.js`, con la ruta al repositorio remoto:

   .. code-block:: 
       :emphasize-lines: 2

       export default defineConfig({
            base: "/dashboard/",
            plugins: ... ,
       })

4. Desde la línea de comandos, ejecute el comando de transpilación y despliegue del sitio web, con:

   .. code-block:: bash

      npm run deploy

   a) De ser necesario, elimine, corrija o comente las secciones de código identificadas por el transpilador.
   b) Vuelva a ejecutar el comando de transpilación y despliegue del sitio web.

5. Compruebe el resultado en el navegador, con la URL: `https://<username>.github.io/dashboard`

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Today we&#39;re sharing that View Transitions and Activity are ready to try in the experimental channel, along with docs and updates on other areas we&#39;re actively working on:<a href="https://t.co/nQqndWzbdX">https://t.co/nQqndWzbdX</a></p>&mdash; React (@reactjs) <a href="https://twitter.com/reactjs/status/1915082330806407433?ref_src=twsrc%5Etfw">April 23, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>