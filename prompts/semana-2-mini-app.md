# Mini-aplicación de práctica: Trivia de cultura general

> **Nota sobre los resultados:** los datos de la Versión A y la Mejora que se identifican como hipotéticos son una reconstrucción plausible para completar la actividad; no son resultados medidos. El modelo concreto no quedó registrado.

## Versión A
**Objetivo:** construir la mini-aplicación con un prompt de una línea.
**Herramienta y modelo:** Copilot con el modelo interactivo (nombre no especificado).
**Prompt:**
```
Haz una app web de trivia con FastAPI.
```
**Resultado (reconstrucción hipotética):** produjo una página básica de trivia, pero dejó incompletos algunos requisitos de la API y el manejo de errores. Se estiman 3 de 6 pruebas aprobadas y 2 errores de Ruff. No se cuenta con un registro real de esta ejecución.

## Versión B
**Objetivo:** construir la misma aplicación con un prompt estructurado, AGENTS.md y pruebas de aceptación.
**Herramienta y modelo:** Copilot con el modelo interactivo (nombre no especificado).
**Prompt:**
```
Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

Objetivo
Construir la mini-aplicación web Trivia de cultura general con estos requisitos:

GET / muestra una página que presenta las preguntas una por una, con cuatro botones de opción, indica si la respuesta fue correcta y muestra el puntaje acumulado.
GET /api/preguntas devuelve una lista de 5 preguntas de cultura general. Cada pregunta tiene los campos id (entero), texto (texto) y opciones (lista de 4 textos). La respuesta correcta no se incluye.
POST /api/responder recibe {"id": 1, "opcion": 2}, donde opcion es un índice de 0 a 3, y devuelve {"correcta": true o false, "respuesta_correcta": índice de 0 a 3}.
Si el id no existe, responde con el código 404. Si la opción no está entre 0 y 3, responde con el código 422.

Contexto
Lee AGENTS.md. El contrato de la API está en tests/test_aceptacion.py: las rutas, los nombres de los campos y los códigos de estado deben coincidir con esas pruebas.

Restricciones
Usa solo las dependencias de requirements.txt. Define las rutas en app/main.py y la lógica en app/servicios.py, sin importar FastAPI en servicios. Guarda los datos en memoria, sin base de datos ni archivos. No modifiques tests/test_aceptacion.py. La página usa HTML, CSS y JavaScript sin librerías externas.

Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a crear y espera mi aprobación. Al terminar, resume en una línea qué hace cada archivo.

Ejemplo
GET /api/preguntas devuelve: [{"id": 1, "texto": "¿Cuál es el planeta más grande del sistema solar?", "opciones": ["Marte", "Júpiter", "Saturno", "Venus"]}, ...]
POST /api/responder con {"id": 1, "opcion": 1} devuelve: {"correcta": true, "respuesta_correcta": 1}

Criterio de éxito
python -m pytest -v pasa todas las pruebas y ruff check . no reporta errores. Si después de 3 intentos las pruebas no pasan, detente y explica el problema.
```
**Resultado:** implementó la trivia con preguntas presentadas una por una, evaluación de respuestas y puntaje acumulado. Según el reporte compartido: 6 pruebas aprobadas, Ruff sin errores y prueba manual en navegador con respuestas correctas e incorrectas. Para completar el dato de intentos, se estima hipotéticamente que necesitó 2 intentos; ese número no fue registrado.

## Mejora
**Objetivo:** permitir elegir entre 1 y 5 preguntas y solicitar esa cantidad a la API.
**Herramienta y modelo:** Copilot con el modelo interactivo (nombre no especificado).
**Prompt:**
```
## Rol
Actúa como desarrollador backend con experiencia en FastAPI, Jinja2 y pruebas con pytest.

## Objetivo
Construir la mini-aplicación web Trivia de cultura general con estos requisitos:
1. GET / muestra una página que presenta las preguntas una por una, con cuatro botones de opción, indica si la respuesta fue correcta y muestra el puntaje acumulado. La página permite elegir cuántas preguntas se jugarán.
2. GET /api/preguntas devuelve una lista de preguntas de cultura general. Cada pregunta tiene los campos id (entero), texto (texto) y opciones (lista de 4 textos). La respuesta correcta no se incluye.
3. GET /api/preguntas acepta el parámetro opcional cantidad, que indica cuántas preguntas devolver. cantidad debe ser un entero entre 1 y 5, inclusive; sin el parámetro, devuelve 5 preguntas. Si cantidad está fuera de ese rango, responde con el código 422.
4. POST /api/responder recibe {"id": 1, "opcion": 2}, donde opcion es un índice de 0 a 3, y devuelve {"correcta": true o false, "respuesta_correcta": índice de 0 a 3}.
5. Si el id no existe, responde con el código 404. Si la opción no está entre 0 y 3, responde con el código 422.

## Contexto
Lee AGENTS.md. El contrato de la API está en tests/test_aceptacion.py: las rutas, los nombres de los campos y los códigos de estado deben coincidir con esas pruebas.

## Restricciones
- Usa solo las dependencias de requirements.txt.
- Define las rutas en app/main.py y la lógica en app/servicios.py, sin importar FastAPI en servicios.
- Guarda los datos en memoria, sin base de datos ni archivos.
- No modifiques tests/test_aceptacion.py.
- La página usa HTML, CSS y JavaScript sin librerías externas.
- La cantidad elegida en la página debe estar entre 1 y 5 y coincidir con la cantidad de preguntas solicitada a la API.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a crear y espera mi aprobación. Al terminar, resume en una línea qué hace cada archivo.

## Ejemplos
GET /api/preguntas devuelve 5 preguntas por defecto.
GET /api/preguntas?cantidad=3 devuelve 3 preguntas.
GET /api/preguntas?cantidad=6 responde con el código 422.
Una pregunta de GET /api/preguntas tiene este formato: [{"id": 1, "texto": "¿Cuál es el planeta más grande del sistema solar?", "opciones": ["Marte", "Júpiter", "Saturno", "Venus"]}, ...]
POST /api/responder con {"id": 1, "opcion": 1} devuelve: {"correcta": true, "respuesta_correcta": 1}

## Criterio de éxito
python -m pytest -v pasa todas las pruebas, incluyendo las de cantidad por defecto, valores válidos y valores fuera de rango, y ruff check . no reporta errores. Si después de 3 intentos las pruebas no pasan, detente y explica el problema.
```
**Resultado (reconstrucción hipotética):** agregó la selección de cantidad en la página y el parámetro `cantidad` en la API, con validación del rango de 1 a 5. Se estima que la primera ejecución omitió el límite máximo en la interfaz y que, tras corregirlo, aprobó 9 de 9 pruebas con 0 errores de Ruff. No se cuenta con un registro real de esta ejecución.

## Comparación
En esta reconstrucción, la Versión A aprueba 3 de 6 pruebas y presenta 2 errores de Ruff; la Versión B aprueba las 6 pruebas reportadas y Ruff no presenta errores; y la Mejora aprueba hipotéticamente 9 de 9 pruebas, también sin errores de Ruff. La comparación sugiere que un prompt estructurado con contexto, restricciones y criterios verificables produce una solución más completa y facilita comprobarla; añadir requisitos concretos y pruebas para la mejora ayuda a detectar y corregir casos límite. Los datos hipotéticos de A y la Mejora, así como el número de intentos de B, deben reemplazarse por resultados reales si se ejecutan las pruebas.
