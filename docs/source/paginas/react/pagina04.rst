..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

==================================
React - Hooks (useEffect)
==================================

.. topic:: Objetivo específico
    :class: objetivo

    Implementar la gestión efectos secundarios y la actualización dinámica de la interfaz según los cambios de ubicación o preferencias del usuario en el dashboard. 

Actividades previas
=====================

Open-Meteo
----------

1. Acceda al sitio `Open-Meteo API <https://open-meteo.com/en/docs>`_.
2. Configure el API de Open-Meteo:
   
   a) En la sección **Location and Time**, seleccione la zona de _America/Chicago (GMT-5)_.
   b) Marque los indicadores: temperatura (`Temperature (2 m)`), humedad relativa (`Relative Humidity (2 m)`), temperatura aparente (`Apparent Temperature`) y  velocidad del viento (`Wind Speed (10 m)`), en la sección **Current Weather** .
   c) En **Settings**, escoja la configuración de las unidades de medida de la API, en este caso: temperatura (`Celsius °C`), velocidad del viento (`km/h`) y unidades de precipitación (`Millimeter`).  

3. Compruebe la estructura del JSON en su navegador.

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

Tipos de datos e Interfaces
---------------------------

1. Acceda al sitio `Transform Tools / JSON to TypeScript <https://transform.tools/json-to-typescript>`_. 
2. Utilice el JSON de salida de la API de Open-Meteo para generar las interfaces de TypeScript. 
3. Dentro de su proyecto *dashboard*:

   a) Cree el archivo `src/types/DashboardTypes.tsx`
   b) Coloque el código de las interfaces generadas en el paso anterior y modifique el nombre de la interfaz `Root` por `OpenMeteoResponse`.

4. Utilice su cliente de IAG para justificar el uso de las interfaces y el tipo de datos que representan.

IndicatorUI
-----------

1. Revise la documentación del componente `Card <https://mui.com/material-ui/react-card/>`_.
2. Cree el componente funcional `IndicatorUI` en el archivo `src/components/IndicatorUI.tsx`, con el siguiente código:
  
   .. code-block:: tsx
       :emphasize-lines: 1-23

        import Card from '@mui/material/Card';
        import CardContent from '@mui/material/CardContent';
        import Typography from '@mui/material/Typography';

        interface IndicatorUIProps {
            title?: string;
            description?: string;
        }

        export default function IndicatorUI(props: IndicatorUIProps) {
            return (
                <Card>
                    <CardContent sx={{ height: '100%' }}>
                    <Typography variant="h5" component="div">
                        {props.description}
                    </Typography>
                    <Typography variant="body2" component="p" color="text.secondary">
                        {props.title}
                    </Typography>
                    </CardContent>
                </Card>
            )
        }

3. Modifique el archivo `src/App.tsx`, con:

   a) Importe el componente `IndicatorUI` desde el archivo `./components/IndicatorUI`.
   b) En la sección en la seccion **Indicadores**:

      (i) Convierta el componente Grid un _contenedor_.
      (ii) Agregue cuatro componentes `IndicatorUI` con los indicadores *Temperatura (2m)*, *Temperatura aparente*, *Velocidad del viento* y *Humedad relativa*.

   .. code-block:: tsx
       :emphasize-lines: 2, 12-30

       ...
       import IndicatorUI from './components/IndicatorUI';
       ...

       function App() {

            ...
            return (
                <Grid ... >

                    {/* Indicadores */}
                    <Grid container size={{ xs: 12, md: 9 }} >

                        <Grid size={{ xs: 12, md: 3 }}>
                            <IndicatorUI title='Temperatura (2m)' description='XX°C' />
                        </Grid>

                        <Grid size={{ xs: 12, md: 3 }}>
                            {/* IndicatorUI con la Temperatura aparente en °C' */}
                        </Grid>

                        <Grid size={{ xs: 12, md: 3 }}>
                            {/* IndicatorUI con la Velocidad del viento en km/h' */}
                        </Grid>
                        
                        <Grid size={{ xs: 12, md: 3 }}>
                            {/* IndicatorUI con la Humedad relativa en %' */}
                        </Grid>

                    </Grid>

                </Grid>
            )
       }

4. Complete los componentes `IndicatorUI` con los valores de los indicadores y sus unidades.
5. Compruebe la vista previa del resultado en el navegador.

React - Hook: useEffect
-----------------------

.. note::

    Considere la explicación del uso del hook `useEffect <https://es.react.dev/reference/react/useEffect>`_.

useFetchData
^^^^^^^^^^^^

1. Cree el componente funcional `useFetchData` en el archivo `src/hooks/useFetchData.tsx`.
2. Cree el componente `useFetchData`, con:

   a) Importe los hooks `useState` y `useEffect` de React.
   b) Importe la interfaz como tipos de datos (`type`)  `OpenMeteoResponse` del archivo `../types/DashboardTypes.tsx`. 
   c) Declare que el componente `useFetchData` retorna un objeto del tipo `OpenMeteoResponse`.
   
   .. dropdown:: Ver la solución 
        :color: success

        .. code-block:: tsx

            import { useEffect, useState } from 'react';
            import { type OpenMeteoResponse } from '../types/DashboardTypes';

            export default function useFetchData() : OpenMeteoResponse { }

3. Dentro de `useFetchData`:
      
   a) Declare la constante de estado `data` y la función de actualización `setData` del tipo `OpenMeteoResponse` (o `null`). El valor predeterminado es de tipo **null**.
   b) Defina la constante `URL` con el :term:`endpoint` de los datos de Open-Meteo.
   c) Agregue el hook `useEffect` para que reaccione **únicamente** después del primer renderizado del DOM.
   d) Retorne `data` al final del componente.
   
   .. dropdown:: Ver la solución 
        :color: success
        
        .. code-block:: tsx
            :emphasize-lines: 3, 5, 7, 9

            export default function useFetchData() : OpenMeteoResponse | undefined {

                const  URL = 'https://api.open-meteo.com/v1/forecast ... ';

                const [data, setData] = useState<OpenMeteoResponse | undefined>();
                
                useEffect(() => { }, []); // El array vacío asegura que el efecto se ejecute solo una vez después del primer renderizado

                return data;

            }

4. Dentro del función flecha del `useEffect`, realice un requerimiento asíncrono con la URL del endpoint. Al completarse la petición, actualice el estado `data` con la respuesta en formato JSON.

   .. dropdown:: Ver la solución
        :color: success

        .. tab-set::
            
            .. tab-item:: Fetch
        
                .. code-block:: tsx
                    :emphasize-lines: 7 - 16

                    export default function useFetchData() : OpenMeteoResponse | undefined {

                        ...
                        
                        useEffect(() => {

                            try {
                                const response = await fetch(URL);
                                if (!response.ok) {
                                    throw new Error(`HTTP error! status: ${response.status}`);
                                }
                                const jsonData: OpenMeteoResponse = await response.json();
                                setData(jsonData);
                            } catch (error) {
                                console.error('Error fetching data:', error);
                            }
                        
                        }, []); // El array vacío asegura que el efecto se ejecute solo una vez después del primer renderizado

                        return ...;

                    }

            .. tab-item:: Axios

                .. code-block:: tsx
                    :emphasize-lines: 7 - 16

                    abc


5. Con un cliente de IAG, explique el uso del hook useEffect y la configuración del arreglo de dependencias.

App.tsx
^^^^^^^

1. Importe y almacene su salida en una constante `dataFetcherOutput` en el archivo `src/App.tsx`.

   .. code-block:: tsx
       :emphasize-lines: 2,8

       ...
       import useFetchData from './hooks/useFetchData';
       ...

       function App() {

            ...
            const dataFetcherOutput = useFetchData();
            
            return ( ... )
       }

2. Modifique el archivo `src/App.tsx`, con:

   a) En el componente `IndicatorUI` para el indicador *Temperatura (2m)*
   b) Utilice `dataFetcherOutput` para validar el renderizado del indicador con el valor de `temperature_2m` y su unidad. Revise la estructura del JSON.

   .. dropdown:: Ver la solución 
        :color: success
    
        .. code-block:: tsx
            :emphasize-lines: 6-10
    
            ...
            {/* Indicadores */}
            <Grid container size={{ xs: 12, md: 9 }} >

                <Grid size={{ xs: 12, md: 3 }}>
                    {dataFetcherOutput && 
                        (<IndicatorUI     
                            title='Temperatura (2m)' 
                            description={ `${dataFetcherOutput.current.temperature_2m} ${dataFetcherOutput.current_units.temperature_2m}` } />)
                    }
                </Grid>
            ...

3. Renderice los demás indicadores con los datos correspondientes de `dataFetcherOutput`.
4. Compruebe el resultado de la petición asíncrona del navegador.

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

    * ¿Cómo te ayudó la inteligencia artificial generativa a entender el propósito de useEffect y su relación con el ciclo de vida de los componentes en React?

    * ¿Qué decisiones tomaste al integrar useEffect en tu dashboard para ejecutar tareas como peticiones asincrónicas o sincronización de datos?

    * ¿Cómo aseguras que el uso de useEffect en tu proyecto refleja tu comprensión y no una dependencia automática de herramientas generativas, especialmente al enfrentar errores o comportamientos inesperados?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">⚛️ useEffect cheatsheet ↓<br><br>❌ Thinking of useEffect as a lifecycle method.<br><br>✅ Thinking of useEffect as a mechanism to sync data (state/props) with systems that aren’t controlled by React. <a href="https://t.co/v8BK5CLsSn">pic.twitter.com/v8BK5CLsSn</a></p>&mdash; George Moller (@_georgemoller) <a href="https://twitter.com/_georgemoller/status/1714250976947794418?ref_src=twsrc%5Etfw">October 17, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>