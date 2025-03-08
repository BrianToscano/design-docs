# TITULO DEL DESIGN DOC
Link: [Link a este design doc](#)

Author(s): Brian T

Status: [Draft, Ready for review, In Review, Reviewed]

Ultima actualización: 2025-03-08

## Contenido
- Goals
- Non-Goals
- Background
- Overview
- Detailed Design
  - Solucion 1
    - Frontend
    - Backend
  - Solucion 2
    - Frontend
    - Backend
- Consideraciones
- Métricas

## Links
- [Un link](#)
- [Otro link](#)

## Objetivo
_Que y porque estamos haciendo esto?_
para que el bot me de las rutinas de ejercisios del dia en el gimnasio separados por dia de la semana o por grupo muscular 

_Incluye contexto para las personas que no están familiarizadas con el proyecto._
En este chat se mandaran las rutinas de ejercicio de lunes a domingo separados cada dia con ejercicios de diferentes grupos musculares automatizado del grupo musculr que vas a trabajar o ordenado por dia de la semana
_Mantenlo corto, elabora en **Background, Overview y Detailed Design**_

_Añade screenshots / mocks si lo ves necesario_

## Goals
- Goals
## Non-Goals
- Non-Goals

## Background
_Cuál es el contexto de este proyecto?_

_Incluye recursos, como otros design docs si es necesario_

_No escribas acerca de tu diseño o requerimientos aquí_
Muchas veces cuando uno esta famirializado con las rutinas o no cuando toca hacer cambio de rutinas de ejercicios en el gym se olvidan de como era la rutina del dia o que tocaba hacer y con el bot ya automatizado nos ayudariamos a saber que rutinas hacer.
Este proyecto tiene como objetivo desarrollar un bot de Telegram que proporcione rutinas de ejercicios diarias para usuarios interesados en entrenamientos de gimnasio. El bot busca ser una herramienta accesible y práctica para aquellos que desean seguir una rutina estructurada de ejercicios sin la necesidad de revisar manualmente un plan.

## Overview
_Overview a alto nivel de tu propuesta_

_Esta sección debería ser entendible por nuevos miembros de tu equipo que no están relacionados al proyecto_

_Pon detalles en la siguiente sección_
Este proyecto consiste en un bot de Telegram que proporciona una rutina de ejercicios diaria para el gimnasio.

El usuario podrá interactuar con el bot a través de comandos para consultar la rutina correspondiente a cada día de la semana.

Características principales:
Responde con la rutina según el día seleccionado.
Opción para consultar la rutina de cualquier día específico.
Opción para recibir automáticamente la rutina del día actual.
Este bot es ideal para quienes buscan un entrenamiento estructurado sin necesidad de revisar manualmente su plan de ejercicios.

## Detailed Design
_Usa diagramas donde veas necesario_

_Herramientas como [Excalidraw](https://excalidraw.com) son buenos recursos para esto_

_Cubre los cambios principales:_

 _- Cuales son las nuevas funciones que vas a escribir?_
 se usará una única función dia_especifico() que recibirá el nombre del día como parámetro en lugar de escribir una función separada para cada día.
 _- Porque necesitas nuevos componentes?_
  Las rutinas estarán almacenadas en un diccionario, lo que facilitará modificaciones sin afectar la estructura del código.
 _- Hay código que puede ser reusable?_
 Se usará la librería datetime para que el comando /hoy identifique automáticamente la rutina correspondiente.

_No elabores minuciosamente la implementación._

## Solution 1
### Frontend
_Frontend…_
El bot de Telegram no tiene una interfaz gráfica tradicional, ya que funciona dentro de la app de Telegram. La "interfaz" se basa en comandos y botones interactivos.

Interacción del usuario:

Envío de comandos como /start, /rutina, /hoy, /lunes, etc.
Respuesta en texto con la rutina correspondiente.
Menú con botones (Opcional) para seleccionar el día de la rutina.

Tecnologías:

Telegram Bot API
Markdown para formatear mensajes
### Backend
_Backend…_
 El backend estará desarrollado en Python con la librería python-telegram-bot.
  Componentes principales:

Manejador de comandos → Responde a /start, /rutina, /hoy, etc.
Diccionario de rutinas → Almacena las rutinas de cada día.
Función de detección del día → Identifica el día actual y responde con la rutina correcta.
Menú de botones (Opcional) → Para elegir el día de la rutina.

Tecnologías:

python-telegram-bot
datetime para obtener el día actual
logging para manejar errores


## Solution 2
### Frontend
_Frontend…_
En esta solución, el bot tendrá una interacción más dinámica con botones inline en lugar de depender solo de comandos.

 Interacción del usuario:

En lugar de escribir comandos, el usuario recibe un menú interactivo con botones para seleccionar la rutina del día.
Opción para recibir recordatorios automáticos con la rutina del día a una hora específica.
Formateo mejorado de mensajes con negritas y emojis.
 Tecnologías:

Telegram Bot API
Markdown + Emojis para formatear mensajes
InlineKeyboardMarkup para botones interactivos

### Backend
_Backend…_
Esta versión agrega funcionalidades avanzadas:

 Componentes principales:

Menú interactivo con botones → Los usuarios pueden tocar el botón del día que quieren ver.
Manejador de recordatorios → Permite configurar recordatorios automáticos para recibir la rutina cada día a una hora específica.
Almacenamiento de preferencias → Se usa una base de datos SQLite para guardar la configuración del usuario (ej. hora del recordatorio).
Modo conversación → Posibilidad de que el bot haga preguntas para guiar la selección del día.
 Tecnologías:

python-telegram-bot
sqlite3 para almacenamiento
apscheduler para enviar recordatorios automáticos
datetime para obtener el día actual

## Consideraciones
_Preocupaciones / trade-offs / tech debt_
Experiencia del Usuario:

Asegúrarse de que la interacción sea intuitiva y clara con botones y mensajes bien formateados.
Escalabilidad:

Considerar usar bases de datos externas si el proyecto crece y para personalizar rutinas o almacenar preferencias del usuario.
Sincronización del Día:

Verificar que la detección del día actual sea precisa y esté sincronizada con la zona horaria del usuario.
Privacidad y Seguridad:

Proteger la información del usuario y cumple con las leyes de privacidad (ej. RGPD).
Modularidad del Código:

Implementar funciones reutilizables y estructura el código para facilitar la expansión a futuro.
Carga del Servidor:

Asegúrarse de manejar tareas programadas y recordatorios automáticos para evitar retrasos o fallos.
Pruebas y Mantenimiento:

Realizar pruebas continuas y usa monitoreo para corregir errores rápidamente.


## Métricas
_Que información necesitas para validar antes de lanzar este feature?_
Tasa de Interacción:

Mide cuántos usuarios están interactuando activamente con el bot (por ejemplo, cuántos usan comandos como /rutina o /hoy).
Tiempo de Respuesta:

Mide el tiempo que tarda el bot en responder a un comando. Un tiempo de respuesta bajo mejora la experiencia del usuario.
Tasa de Éxito de Comandos:

Mide cuántos comandos son procesados correctamente sin errores. Idealmente, debe ser cercana al 100%.
Frecuencia de Uso:

Analiza con qué frecuencia los usuarios interactúan con el bot. Esto ayuda a determinar si el bot es útil de forma continua.
Retención de Usuarios:

Mide si los usuarios regresan a usar el bot después de su primera interacción. La retención indica el valor percibido del bot.
Satisfacción del Usuario:

Se puede medir mediante encuestas dentro del bot o analizando los comentarios y la retroalimentación de los usuarios.
Tasa de Personalización:

Mide cuántos usuarios configuran características personalizadas (por ejemplo, establecer recordatorios) para evaluar el nivel de personalización del servicio.