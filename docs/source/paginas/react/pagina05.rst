..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

======================================================
React - Gestión y visualización datos (MUI-X)
======================================================

.. topic:: Objetivo específico
    :class: objetivo

    Incorporar componentes avanzados de gestión y visualización de datos para la representación de datos climáticas en tiempo en el dashboard.

Actividades previas
=====================

Open-Meteo
----------

1. Configure API de Open-Meteo en `Open-Meteo API <https://open-meteo.com/en/docs>`_, con:
   
   a) Seleccione la ubicación de una ciudad de Ecuador.
   b) Marque los indicadores que desea mostrar el dashboard en la sección de `Current Weather <https://open-meteo.com/en/docs#current_weather>`_ de la documentación, en este caso: temperatura (`Temperature (2 m)`), humedad relativa (`Relative Humidity (2 m)`), temperatura aparente (`Apparent Temperature`) y  velocidad del viento (`Wind Speed (10 m)`).
   c) Seleccione **dos variables meteorológicas por hora**, por ejemplo: Temperatura (`Temperature (2 m)`) y Velocidad del viento (`Wind Speed (10 m)`), etc.
   d) Seleccione la configuración de las unidades de medida de la API, en este caso: temperatura (`Celsius °C`), velocidad del viento (`km/h`) y unidades de precipitación (`Millimeter`), etc.  

2. Con la URL de la API con los parámetros seleccionados, compruebe la estructura del JSON de salida en su navegador.

Interfaces, tipos de datos y URL
--------------------------------

1. Genere el tipo de datos TypeScript para el JSON de salida de la API de Open-Meteo, con:

   a) Utilice `Transform Tools / JSON to TypeScript <https://transform.tools/json-to-typescript>`_. 
   b) Coloque el JSON de salida de la API de Open-Meteo en el campo de entrada.
   c) Identifique las diferencias con las interfaces existentes en el archivo `src/types/DashboardTypes.tsx`.
   d) Actualice o cree nuevas interfaces en el archivo `src/types/DashboardTypes.tsx`, según sea necesario.

2. Actualice la URL en `hooks/useFetchData.tsx` con la URL generada en Open-Meteo.

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

TableUI y ChartUI
-----------------

1. Instale los paquetes necesarios para la :term:`gestión y visualización de datos`, con:

   .. code-block:: bash

      npm install npm install @mui/x-data-grid @mui/x-charts

2. Revise la documentación `MUI X Data Grid <https://mui.com/x/react-data-grid/>`_  y `MUI X Charts <https://mui.com/x/react-charts/>`_ de MUI X.
3. Cree los componentes funcionales:  

   a) `TableUI` en el archivo `src/components/TableUI.tsx`, con el siguiente código:

   .. dropdown:: Ver el código 
      :color: primary   

      .. code-block:: tsx
         :emphasize-lines: 1-66

         import Box from '@mui/material/Box';
         import { DataGrid, type GridColDef } from '@mui/x-data-grid';

         function combineArrays(arrLabels: Array<string>, arrValues1: Array<number>, arrValues2: Array<number>) {
            return arrLabels.map((label, index) => ({
               id: index,
               label: label,
               value1: arrValues1[index],
               value2: arrValues2[index]
            }));
         }

         const columns: GridColDef[] = [
            { field: 'id', headerName: 'ID', width: 90 },
            {
               field: 'label',
               headerName: 'Label',
               width: 125,
            },
            {
               field: 'value1',
               headerName: 'Value 1',
               width: 125,
            },
            {
               field: 'value2',
               headerName: 'Value 2',
               width: 125,
            },
            {
               field: 'resumen',
               headerName: 'Resumen',
               description: 'No es posible ordenar u ocultar esta columna.',
               sortable: false,
               hideable: false,
               width: 100,
               valueGetter: (_, row) => `${row.label || ''} ${row.value1 || ''} ${row.value2 || ''}`,
            },
         ];

         const arrValues1 = [4000, 3000, 2000, 2780, 1890, 2390, 3490];
         const arrValues2 = [2400, 1398, 9800, 3908, 4800, 3800, 4300];
         const arrLabels = ['A','B','C','D','E','F','G'];

         export default function TableUI() {

            const rows = combineArrays(arrLabels, arrValues1, arrValues2);

            return (
               <Box sx={{ height: 350, width: '100%' }}>
                  <DataGrid
                     rows={rows}
                     columns={columns}
                     initialState={{
                        pagination: {
                           paginationModel: {
                              pageSize: 5,
                           },
                        },
                     }}
                     pageSizeOptions={[5]}
                     disableRowSelectionOnClick
                  />
               </Box>
            );
         }

   b)  `ChartUI` en el archivo `src/components/ChartUI.tsx`, con el siguiente código:

   .. dropdown:: Ver el código 
      :color: primary  

      .. code-block:: tsx
         :emphasize-lines: 1-29

         import { LineChart } from '@mui/x-charts/LineChart';
         import Typography from '@mui/material/Typography';

         const arrValues1 = [4000, 3000, 2000, 2780, 1890, 2390, 3490];
         const arrValues2 = [2400, 1398, 9800, 3908, 4800, 3800, 4300];
         const arrLabels = ['A','B','C','D','E','F','G'];


         export default function ChartUI() {
            return (
               <>
                  <Typography variant="h5" component="div">
                     Chart arrLabels vs arrValues1 & arrValues2
                  </Typography>
                  <LineChart
                     height={300}
                     series={[
                        { data: arrValues1, label: 'value1'},
                        { data: arrValues2, label: 'value2'},
                     ]}
                     xAxis={[{ scaleType: 'point', data: arrLabels }]}
                  />
               </>
            );
         }

5. Importe los componentes `TableUI` y `ChartUI` en el archivo `src/App.tsx`, con:

   .. code-block:: tsx
       :emphasize-lines: 2-3, 15, 20

       ...
       import TableUI from './components/TableUI';
       import ChartUI from './components/ChartUI';

       function App() {

            ...
            return (
                <Grid ... >

                  ...

                  {/* Gráfico */}
                  <Grid size={{ xs: 6, md: 6 }} sx={{ display: { xs: "none", md: "block" } }}>
                     <ChartUI />
                  </Grid>

                  {/* Tabla */}
                  <Grid size={{ xs: 6, md: 6 }} sx={{ display: { xs: "none", md: "block" } }}>
                     <TableUI />
                  </Grid>

                  ...
                
                </Grid>
            )
       }

6. Compruebe la vista previa del resultado en el navegador.

Renderizado
-----------

1. Modifique los componentes `TableUI` y `ChartUI` para que usen los datos de la API de Open-Meteo.
2. Asegúrese de que los datos se muestren correctamente en la tabla y el gráfico, considerando el tiempo de carga y el manejo de errores.
3. Compruebe la vista previa del resultado en el navegador.

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

    * ¿Qué criterios técnicos consideraste al evaluar si las propuestas de la IA para la gestión y visualización de datos eran adecuadas para el tipo de información que tu dashboard necesitaba presentar?

    * ¿Cómo integraste de forma efectiva la visualización de datos con los demás elementos del dashboard, asegurando coherencia visual y funcional entre los componentes sugeridos por la IA y los desarrollados por ti?
    
    * ¿Cómo garantizas que el uso de inteligencia artificial en la configuración de componentes no reste valor a tu propio proceso de diseño y toma de decisiones como desarrollador?


Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">Data visualization guide for creating plots for a data visualization project👍<br><br>Which chart to use in what circumstances?? (See the below image) <a href="https://t.co/6EwcE6Ld9N">pic.twitter.com/6EwcE6Ld9N</a></p>&mdash; Avi Kumar Talaviya (@avikumart_) <a href="https://twitter.com/avikumart_/status/1541534335278338049?ref_src=twsrc%5Etfw">June 27, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>