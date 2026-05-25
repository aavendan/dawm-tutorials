..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===================================
React y MUI - Introducción
===================================

.. topic:: Objetivo específico
    :class: objetivo

    Utilizar React para construir la estructura inicial del dashboard e integrar la librería MUI para incorporar componentes visuales modernos que mejoren la usabilidad e interfaz del sistema.
 

Actividades previas
=====================

Open-Meteo
----------

1. Explore la documentación de la `API de Open-Meteo <https://open-meteo.com/en/docs>`_ para comprender cómo se realizan las solicitudes para obtener datos meteorológicos.
2. Practique haciendo solicitudes a la API utilizando herramientas como cURL o desde una pestaña en su navegador.

Diseño del dashboard
----------------------

1. Identifique los elementos claves del API que serán útiles para el :term:`dashboard`:

   a) **Parámetros de entrada (Input)**: Determine qué parámetros son necesarios para realizar una solicitud a la API, como ubicación geográfica o zona horaria.
   b) **Datos disponibles (Variables climáticas)**: Explore las variables climáticas que la API puede proporcionar y su frecuencia temporal, como temperatura actual, por día o por hora, etc.
   c) **Formato de respuesta (Response)**: Familiarícese con el formato de respuesta de la API, que generalmente es JSON, y cómo se estructuran los datos.
   d) **Codificación del clima (weathercode)**: Comprenda cómo se codifica el clima en la respuesta de la API, lo que le permitirá interpretar correctamente las condiciones climáticas.
   e) **Errores comunes**: Identifique la respuesta de la API para los errores más comunes, como solicitudes mal formadas o problemas de conexión.
   f) **Casos de uso para el dashboard**: Reflexione sobre cómo estos datos pueden ser utilizados en el dashboard, como mostrar el clima actual, pronósticos extendidos, gráficos de evolución, alertas visuales, etc.
      
      (i) Clima actual: temperatura, humedad, estado del cielo
      (ii) Gráficos de evolución: temperatura por hora, precipitación acumulada
      (iii) Pronósticos extendidos: próximos 7 días
      (iv) Alertas visuales: si uv_index_max supera cierto umbral, mostrar advertencia
      (v) Íconos adaptativos: usando weathercode

2. Responda a la actividad en clases del diseño generado.

Ambiente de desarrollo
----------------------

1. Cree un repositorio en GitHub con el nombre *dashboard*.

   a) Agregue un archivo README.md con el título de su dashboard y una breve descripción del objetivo de su proyecto.
   b) Agregue un archivo *.gitignore* con la plantilla de *Node*.
   
2. Acceda a su proyecto *dashboard* en Codespaces o en su máquina local.
3. Cree y utilice la(s) rama(s) de desarrollo.

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
   
   b) Seleccione el framework como :term:`React` y la variante como `TypeScript`.
   c) Instale las dependencias del proyecto e inicie el servidor de desarrollo con los siguientes comandos:

   .. code-block:: bash

      npm install
      npm run dev

3. Compruebe la vista previa del resultado en el navegador.
4. Con un cliente de IAG, explique la estructura del proyecto en React, específicamente por el propósito de los archivos `index.html`, `src/main.tsx` y `src/App.tsx`.

React: App.tsx
--------------

1. Modifique el archivo `src/App.tsx` para mostrar un mensaje de bienvenida, por ejemplo:

   .. code-block:: tsx
      :emphasize-lines: 5-7

      ...

      function App() {
          return (
              <div>
                  <h1>Bienvenido al Dashboard</h1>
              </div>
          );
      }

      export default App;

2. Compruebe la vista previa del resultado en el navegador.
3. Utilice un cliente de IAG, para explicar cómo se renderiza el componente principal de la aplicación y :term:`JSX`.

MUI: Inicialización del proyecto y componente Grid
--------------------------------------------------

1. Explore la documentación de `MUI <https://mui.com/material-ui/getting-started/overview/>`_ para comprender cómo integrar esta biblioteca en su proyecto de React.
2. Instale MUI y sus dependencias en su proyecto de React con el siguiente comando:

   .. code-block:: bash

      npm install @mui/material @emotion/react @emotion/styled

3. Importe el componente `Grid` de MUI en su archivo `src/App.tsx` y utilícelo para crear una estructura básica de cuadrícula para su dashboard:

   .. code-block:: tsx
      :emphasize-lines: 2, 6-29

      ...
      import { Grid } from '@mui/material';

      function App() {
         return (
            <Grid>

               {/* Encabezado */}
               <Grid>Elemento: Encabezado</Grid>

               {/* Alertas */}
               <Grid>Elemento: Alertas</Grid>

               {/* Selector */}
               <Grid>Elemento: Selector</Grid>

               {/* Indicadores */}
               <Grid>Elemento: Indicadores</Grid>

               {/* Gráfico */}
               <Grid>Elemento: Gráfico</Grid>

               {/* Tabla */}
               <Grid>Elemento: Tabla</Grid>

               {/* Información adicional */}
               <Grid>Elemento: Información adicional</Grid>

            </Grid>
         );
      }

      export default App;

4. Compruebe la vista previa del resultado en el navegador. 
5. Con un cliente de IAG, explique cómo se utiliza el componente `Grid` de MUI para crear una estructura de cuadrícula y cómo se pueden agregar elementos dentro de esta cuadrícula.

MUI: Ubicación de elementos y Responsividad
-------------------------------------------

1. Modifique el componente `Grid` de su archivo `src/App.tsx`:

   a) Para que sea un contenedor principal utilizando el :term:`prop` `container <https://mui.com/material-ui/react-container/>`_.
   b) Ajuste el espaciado de 5 unidades entre los elementos utilizando la propiedad `spacing <https://mui.com/material-ui/react-container/>`_. 
   c) Centre los todos los elementos con utilizando las propiedades `justifyContent y alignItems <https://mui.com/material-ui/react-grid/#centered-elements>`_.
   d) Compruebe la vista previa del resultado en el navegador.
   
   
   .. code-block:: tsx
      :emphasize-lines: 5

      ...

      function App() {
         return (
            <Grid container spacing={5} justifyContent="center" alignItems="center">
               ...
            </Grid>
         );
      }

2. :material-round:`note_alt;1.5em;sd-text-success` Revise la documentación de `fluid grids <https://mui.com/material-ui/react-grid/#fluid-grids>`_ en MUI, para aplicar el estilo:

   a) Pantallas extra pequeñas `xs`, todos los elementos ocupan 12 columnas. 
   b) Pantallas medianas `md`, en adelante:
   
      (i) El encabezado ocupe todo el ancho (12 columnas), 
      (ii) Las alertas ocupan 12 columnas.
      (iii) El selector ocupa 3 columnas y los indicadores ocupan 9 columnas.
      (iv) El gráfico ocupa 6 columnas y la tabla ocupa 6 columnas.
      (v) El elemento de información adicional ocupan 12 columnas.

   c) Compruebe la vista previa del resultado en el navegador.

   .. dropdown:: Ver el código 
      :color: primary

      .. code-block:: tsx
         :emphasize-lines: 8, 13, 16

         ...

         function App() {
            return (
               <Grid ... >

                  {/* Encabezado */}
                  <Grid size={{ xs: 12, md: 12 }}>Elemento: Encabezado</Grid>

                  ...

                  {/* Selector */}
                  <Grid size={{ xs: 12, md: 3  }}>Elemento: Selector</Grid>

                  {/* Indicadores */}
                  <Grid size={{ xs: 12, md: 9 }}>Elemento: Indicadores</Grid>

                  ...

               </Grid>
            );
            }

         export default App;

3. :material-round:`note_alt;1.5em;sd-text-success` Revise la documentación de la propiedad `sx <https://mui.com/material-ui/customization/how-to-customize/#the-sx-prop>`_, para que la gráfica y la tabla no se muestran en pantallas extra pequeñas y se muestran como bloque desde pantallas medianas.

   .. dropdown:: Ver el código 
      :color: primary

      .. code-block:: tsx
         :emphasize-lines: 11,17

         ...

         function App() {
            return (
               <Grid ... >

                  ...

                  {/* Gráfico */}
                  <Grid ... 
                     sx={{ display: { xs: "none", md: "block"} }} >
                     Elemento: Gráfico
                  </Grid>

                  {/* Tabla */}
                  <Grid ... 
                     sx={{ display: { xs: "none", md: "block" } }}>
                     Elemento: Tabla
                  </Grid>

                  ...

               </Grid>
            );
         }

         export default App;

4. Compruebe la vista previa del resultado en el navegador para diferentes tamaños.
5. Consulte su cliente de IAG para explicar la utilidad de los props en los componentes, por ejemplo `size` y `sx`.

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

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Cómo te ayudó la inteligencia artificial generativa a comprender los principios de diseño de interfaces con React y MUI, como la reutilización de componentes y la jerarquía visual?

    * ¿Cómo aseguraste que la interacción entre los componentes de React y los estilos de MUI generados por la IA fueran consistentes, accesibles y adaptables en distintos tamaños de pantalla?

    * ¿Qué actitudes consideras fundamentales para asegurar que el resultado final del dashboard sea auténtico y producto de tu criterio profesional, incluso si partiste de una base generada por IA?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

   <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Today we&#39;re sharing that View Transitions and Activity are ready to try in the experimental channel, along with docs and updates on other areas we&#39;re actively working on:<a href="https://t.co/nQqndWzbdX">https://t.co/nQqndWzbdX</a></p>&mdash; React (@reactjs) <a href="https://twitter.com/reactjs/status/1915082330806407433?ref_src=twsrc%5Etfw">April 23, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>