..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===============================================
Guía 17: React - Comunicación entre componentes
===============================================

.. topic:: Objetivo específico
    :class: objetivo

    Implementar una estrategia de comunicación entre componentes en React utilizando hooks personalizados para la gestión de estados y efectos secundarios. 

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

Comunicación entre componentes con hooks personalizados
-------------------------------------------------------

1. Analice el siguiente escenario de interacción en el dashboard: 

   a) El usuario selecciona una ciudad de la lista de opciones.
   b) El sistema realiza una petición asincrónica a una API de datos climáticos para obtener la información correspondiente a la ciudad seleccionada.
   c) De acuerdo con la respuesta de la API, el sistema actualiza los componentes visuales del dashboard, incluyendo indicadores, tablas y gráficos, para reflejar los datos climáticos de la ciudad seleccionada.

2. Genere el código necesario para implementar este escenario en su proyecto *dashboard*.

   a) En el componente `App.tsx`:
 
   .. code-block:: typescript
       :emphasize-lines: 1, 6-7, 9-10, 15

       import { useState } from 'react';
       ...

       function App() {
        
         // Utilice una variable de estado para almacenar la opción seleccionada por el usuario
         const [selectedOption, setSelectedOption] = useState<string | null>(null);

         // Comunique la opción seleccionada al hook useFetchData
         const dataFetcherOutput = useFetchData(selectedOption);

         return (

            ...
            <SelectorUI onOptionSelect={setSelectedOption} />
            ...

         );
        
       }

   b) En el componente `SelectorUI.tsx`:

   .. code-block:: typescript
       :emphasize-lines: 3-6, 8-9, 16-17
    
       ...
    
       // Defina la interfaz del prop
       interface SelectorProps {
          onOptionSelect: (option: string) => void; 
       }
    
       // Defina el prop en el componente
       export default function Selector({ onOptionSelect }: SelectorProps) {
          
            ...
    
            const handleChange = (event: SelectChangeEvent<string>) => {
              ...

              // Comunique los cambios al componente padre
              onOptionSelect(selectedValue); 

            };
    
            ...
       }

   c) En el hook `useFetchData.tsx`:

   .. code-block:: typescript
       :emphasize-lines: 3-7, 9-10, 17-19, 24

       ...

       // Estrategia para convertir la opción seleccionada en un objeto
       const CITY_COORDS: Record<string, { latitude: number; longitude: number }> = {
         'guayaquil': { latitude: -2.1962, longitude: -79.8862 },
         ...
       };

       // Tipo del prop: string | null
       export default function useFetchData(selectedOption: string | null) : OpenMeteoResponse {
        
         ...

         useEffect(() => {
           

           // Parametrice la opción seleccionada en la URL del requerimiento asíncrono
           const cityConfig = selectedOption != null? CITY_COORDS[selectedOption] : CITY_COORDS["guayaquil"];
           const URL = `https://api.open-meteo.com/v1/forecast?latitude=${cityConfig.latitude}&longitude=${cityConfig.longitude}&...`

           fetch( URL )
           ...
           
         }, [selectedOption]); // El efecto secundario depende de la opción seleccionada
        
         ...
       }

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

    * ¿Cómo te ayudó la inteligencia artificial generativa a entender la comunicación entre componentes en React?

    * ¿Qué decisiones tomaste al integrar un hook para personalizar la interacción en tu dashboard?

    * ¿Cómo aseguras que el uso de hooks en tu proyecto refleja tu comprensión y no una dependencia automática de herramientas generativas, especialmente al enfrentar errores o comportamientos inesperados?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">⚛️ React tip: typing custom hooks return values using TypeScript ↓ <a href="https://t.co/gUCnG3P5m3">pic.twitter.com/gUCnG3P5m3</a></p>&mdash; George Moller (@_georgemoller) <a href="https://twitter.com/_georgemoller/status/1749603458527744106?ref_src=twsrc%5Etfw">January 23, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>