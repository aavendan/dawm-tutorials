..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===============================================
React - Componentes, Interfaces y Props 
===============================================

.. topic:: Objetivo específico
    :class: objetivo

    Desarrollar componentes funcionales reutilizables en React que se comuniquen mediante props, tipadas con interfaces en TypeScript, asegurando una arquitectura modular y mantenible del dashboard.

Actividades previas
=====================

Ambiente de desarrollo
----------------------

1. Acceda a su proyecto *dashboard* en Codespaces o en su máquina local.
2. Cree y utilice la(s) rama(s) de desarrollo.
3. Instale los paquetes y levante el servidor, con:

   .. code-block:: bash

      npm install
      npm run dev

Actividades en clases
=====================

React y MUI: Componentes y Props
---------------------------------

.. note::

   Utilice la documentación de `TypeScript <https://www.typescriptlang.org/docs/handbook/intro.html>`_, de `React <https://es.react.dev/learn>`_ y de `Material UI components <https://mui.com/material-ui/all-components/>`_.

Componente: HeaderUI
^^^^^^^^^^^^^^^^^^^^

1. Cree y exporte el :term:`componente funcional` **HeaderUI** en el archivo `src/components/HeaderUI.tsx`.
2. Agregue el contenido al componente `HeaderUI`, con:

   a) Importe el componente `Typography <https://mui.com/material-ui/react-typography/>`_ de la librería `@mui/material/Typography`
   b) En el JSX, use el componente `Typography` con las siguientes propiedades:
      
      (i) Estilo tipográfico (variant) de un encabezado de nivel 2 (h2),
      (ii) Renderización (component) como un encabezado de nivel 1 (h1), y
      (iii) Estilo en línea (sx) para que el texto se muestre en negrita (fontWeight: 'bold').

   c) El texto del componente `Typography` es "Dashboard del Clima".  

   .. dropdown:: Ver la solución 
        :color: success

        .. code-block:: tsx
            :emphasize-lines: 1-12

            import Typography from '@mui/material/Typography';

            export default function HeaderUI() {
                return (
                    <Typography 
                        variant="h2" 
                        component="h1" 
                        sx={{fontWeight: 'bold'}}>
                        Dashboard del Clima
                    </Typography>
                )
            }

3. Modifique el archivo `src/App.tsx`, con: 

   a) Importe el componente `HeaderUI`.
   b) Use el componente `HeaderUI` dentro de la sección **Encabezado**.

   .. code-block:: tsx
       :emphasize-lines: 2,11

       ...
       import HeaderUI from './components/HeaderUI';

       function App() {
            
            return (
                <Grid ... >

                {/* Encabezado */}
                <Grid ... >
                    <HeaderUI/>
                </Grid>

                ...
            )
        }

4. Compruebe la vista previa del resultado en el navegador.
5. Con un cliente de IAG, compare el uso del DOM versus el uso del DOM Virtual de React.

Interfaz: AlertConfig
^^^^^^^^^^^^^^^^^^^^^

1. Cree y exporte el componente funcional **AlertUI** en el archivo `src/components/AlertUI.tsx`.
2. Agregue el contenido al componente `AlertUI`, con:
    
   a) Importe el componente `Alert <https://mui.com/material-ui/react-alert/>`_ desde la librería `@mui/material/Alert`.
   b) Define la :term:`interfaz` **AlertConfig**, con la propiedad `description` del tipo cadena de texto.
   c) Agregue el parámetro `config` del tipo **AlertConfig** a componente funcional `AlertUI`.
   d) En el JSX, use el component `Alert` con las siguientes propiedades:
      
      (i) El tipo de alerta de éxito (severity=\"success\"),
      (ii) El estilo visual del componente es contorneado (variant=\"outlined\"),
      (iii) Renderice el valor de parámetro `description` (config.description) como contenido del componente.

   .. dropdown:: Ver la solución 
        :color: success

        .. code-block:: tsx
            :emphasize-lines: 1-11

            import Alert from '@mui/material/Alert';

            interface AlertConfig {
                description: string;
            }

            export default function AlertUI( config:AlertConfig ) {
                return (
                    <Alert variant="standard" severity="success"> {config.description} </Alert>
                )
            }

3. Modifique el archivo `src/App.tsx`, con:

   a) Importe el componente `AlertUI`
   b) Use el componente `AlertUI`, pase el prop `description` con el valor 'No se preveen lluvias'
   c) Convierta el elemento `Grid` en un contenedor, alinea horizontalmente los elementos al borde derecho y alinea verticalmente al centro del eje transversal. 

   .. code-block:: tsx
       :emphasize-lines: 2,11,13

       ...
       import AlertUI from './components/AlertUI';

       function App() {
            
            return (
                <Grid ... >

                {/* Alertas */}
                <Grid ...
                    container sx={{ justifyContent: "center", alignItems: "center" }}>
                    
                    <AlertUI description="No se preveen lluvias"/>
                
                </Grid>

                ...
            )
        }


4. Compruebe la vista previa del resultado en el navegador.
5. Con un cliente de IAG genere el código para modificar los props `variant` y `severity` desde el componente padre.

Versionamiento
--------------

1. Versione local y remotamente la(s) rama(s) de desarrollo en el repositorio *dashboard*.
2. Genere la(s) solicitud(es) de cambios (pull request) para la rama principal y apruebe los cambios.

Despliegue
----------

1. Desde la línea de comandos, ejecute el comando de transpilación y despliegue del sitio web, con:

   .. code-block:: bash

      npm run deploy

   a) De ser necesario, elimine, corrija o comente las secciones de código identificadas por el transpilador.
   b) Vuelva a ejecutar el comando de transpilación y despliegue del sitio web.

2. Compruebe el resultado en el navegador, con la URL: `https://<username>.github.io/dashboard`

Conclusiones
============

.. topic:: Preguntas de cierre

    * ¿Qué aspectos de la definición de interfaces y tipos de props crees que podrían malinterpretarse si solo se confía en las sugerencias de la IA sin reflexionar sobre el contexto del componente?

    * ¿Cómo comprobaste que los componentes creados con interfaces propias fueran reutilizables y escalables dentro de la estructura general del dashboard?

    * ¿Cómo equilibras el apoyo recibido por la IA con tu responsabilidad como desarrollador para comprender y justificar el uso de props e interfaces en cada componente del dashboard?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html
    
    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">I draw my mental schema of a <a href="https://twitter.com/reactjs?ref_src=twsrc%5Etfw">@reactjs</a> component. Here&#39;s what it looks like! Let&#39;s dig in!<br><br>🧵 Thread: Anatomy of a React Component (1/5) <a href="https://t.co/jeeKGXXu0G">pic.twitter.com/jeeKGXXu0G</a></p>&mdash; Baptiste Adrien (@baptadn) <a href="https://twitter.com/baptadn/status/1808149818763616748?ref_src=twsrc%5Etfw">July 2, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>