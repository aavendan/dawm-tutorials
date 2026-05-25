..
   Copyright (c) 2025 Allan Avendaño Sudario
   Licensed under Creative Commons Attribution-ShareAlike 4.0 International License
   SPDX-License-Identifier: CC-BY-SA-4.0

===========================================
React - Eventos y Hooks (useState)
===========================================

.. topic:: Objetivo específico
    :class: objetivo

    Gestionar la interactividad del dashboard mediante eventos del usuario y el uso de hooks como useState y useRef, permitiendo actualizar el estado de la interfaz de forma reactiva y eficiente. 

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

React: Eventos y Hooks
----------------------

.. note::

    Considere la explicación del uso de hooks en `React Hooks - Tutorial <https://adictosaltrabajo.com/2020/02/06/react-hooks-tutorial/>`_ y del manejo de eventos en `Tutorial React: Eventos en React <https://certidevs.com/tutorial-react-eventos-y-manejo-de-eventos>`_.

Selector
^^^^^^^^

1. Cree el archivo `src/components/SelectorUI.tsx`.
2. Utilice la documentación del componente `Select <https://mui.com/material-ui/react-select/>`_ para crear el componente funcional `SelectorUI`, con el siguiente código:

   .. code-block:: tsx
       :emphasize-lines: 1-25

       import FormControl from '@mui/material/FormControl';
       import InputLabel from '@mui/material/InputLabel';
       import Select from '@mui/material/Select';
       import MenuItem from '@mui/material/MenuItem';

       export default function SelectorUI() {
    
       return (
          <FormControl fullWidth>
             <InputLabel id="city-select-label">Ciudad</InputLabel>
             <Select
                labelId="city-select-label"
                id="city-simple-select"
                label="Ciudad">
                <MenuItem disabled><em>Seleccione una ciudad</em></MenuItem>
                <MenuItem value={"guayaquil"}>Guayaquil</MenuItem>
                <MenuItem value={"quito"}>Quito</MenuItem>
                <MenuItem value={"manta"}>Manta</MenuItem>
                <MenuItem value={"cuenca"}>Cuenca</MenuItem>
             </Select>

          </FormControl>
          )
       }

3. En el archivo `src/App.tsx`, importe y use el componente `SelectorUI` en la sección para el **Selector**.
4. Compruebe la vista previa del resultado en el navegador.
5. Con un cliente de IAG, compare el uso del DOM versus el uso del DOM Virtual de React.

Evento: onChange
^^^^^^^^^^^^^^^^

1. Utilice su cliente de IAG, para modificar el componente `SelectorUI` con el siguiente código:

   a) Importe el tipo `SelectChangeEvent` desde la librería `@mui/material/Select`
   b) Dentro del componente `SelectorUI`, declare una función flecha `handleChange`, que:
   
      (i) Recibe el parámetro **event** de tipo `SelectChangeEvent<string>` 
      (ii) Muestra en una ventana emergente el valor actual del elemento que generó el evento.

   c) Modifique el componente `Select` de MUI para asignar la función `handleChange` al evento `onChange`.

   .. dropdown:: Ver la solución 
        :color: success

        .. code-block:: tsx
            :emphasize-lines: 2,7-9,15

            ...
            import Select, { type SelectChangeEvent } from '@mui/material/Select';
            ...

            export default function SelectorUI() {
                
                const handleChange = (event: SelectChangeEvent<string>) => {
                    alert(event.target.value)
                };

                return (
                    ...
                    <Select
                        ...
                        onChange={handleChange} >
                        ...
                    </Select>
                    ...
                )
            }

2. Compruebe la vista previa del resultado en el navegador.
3. Con un cliente de IAG, explique la sintaxis y manejo de eventos sintéticos en React.

Hooks: useState
^^^^^^^^^^^^^^^^

1. Utilice su cliente de IAG, para modificar el componente `SelectorUI` con el siguiente código:

   a) Importe el :term:`hook` **useState** desde la librería de React para poder manejar el estado interno del componente.
   b) Dentro del componente, declare una :term:`variable de estado` llamada **cityInput** junto con su :term:`función de actualización` **setCityInput**. 
   c) Dentro de la función `handleChange`, reemplace el código anterior por una llamada a la función de actualización `setCityInput` con el valor seleccionado (event.target.value).
   d) En el `<Select>`, enlace el prop value con la variable de estado `cityInput`.
   e) Debajo del `<Select>`, solamente si `cityInput` tiene un valor muestre un párrafo con el texto 'Información del clima en [ciudad seleccionada]'. Aplica el estilo para mostrar el nombre de la ciudad en negritas y la primera letra en mayúsculas.

   .. dropdown:: Ver la solución 
        :color: success

        .. code-block:: tsx
            :emphasize-lines: 2,6,9,16,20-24

            ...
            import { useState } from 'react';

            export default function SelectorUI() {

                const [cityInput, setCityInput] = useState('');

                const handleChange = (event: SelectChangeEvent<string>) => {
                    setCityInput(event.target.value)
                };

                return (
                    ...
                    <Select
                        ...
                        value={cityInput}>
                        ...
                    </Select>

                    {cityInput && (
                        <p>
                            Información del clima en <span style={{textTransform: 'capitalize', fontWeight: 'bold'}}>{cityInput}</span>
                        </p>
                    )}
                    ...
                )
            }

2. Compruebe la vista previa del resultado en el navegador.
3. Con un cliente de IAG, explique el propósito de los hooks y de useState en React.

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

    * ¿Cómo te ayudó la inteligencia artificial generativa a entender la relación entre los eventos onChange y el hook useState al capturar y actualizar datos en tiempo real dentro de un componente?

    * ¿Qué ajustes tuviste que realizar al código propuesto por la IA para lograr que el evento onChange actualizara correctamente el estado mediante useState en tu dashboard?

    * ¿Cómo puedes demostrar que comprendes y eres responsable del código que usas, incluso si fue generado por IA, particularmente cuando se trata de funcionalidades interactivas como la gestión de estado?

Actividades autónomas
=====================

Recursos extras
------------------------------

En redes:

.. raw:: html

    <blockquote class="twitter-tweet"><p lang="en" dir="ltr">⚛️ Massive React hooks cheatsheet ↓ <br><br>1/8 <a href="https://t.co/S0BPD9OHrf">pic.twitter.com/S0BPD9OHrf</a></p>&mdash; George Moller (@_georgemoller) <a href="https://twitter.com/_georgemoller/status/1748347605606600820?ref_src=twsrc%5Etfw">January 19, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
