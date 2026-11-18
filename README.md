# Problema-2-Red-de-polinizadores
Un polinizador recorre un cultivo de flores con energía limitada, viento y zonas de riesgo. Debe elegir una ruta que maximice el néctar recolectado mientras minimiza el gasto energético. La API planifica la ruta óptima y calcula el costo de energía y la probabilidad de éxito del recorrido.

## Descripción

El proyecto representa los datos de entrada del problema en `cultivo.json`. El archivo
describe el campo, las flores disponibles, las condiciones ambientales y las
capacidades del polinizador.

## Contenido de `cultivo.json`

### `cultivo`

Define las dimensiones y el nombre del área de cultivo.

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `ancho` | número | Anchura del área de cultivo. |
| `alto` | número | Altura del área de cultivo. |
| `nombre` | texto | Nombre identificador del cultivo. |
| `obstaculos` | lista | Conjunto de obstáculos presentes dentro del cultivo.

Cada elemento de `obstaculos` contiene `x`, `y`, `radio` y `descripcion`.  Los obstaculos representa elementos que pueden dificultar el movimiento de los polinizadores.

### `flores`

Es una lista de flores que el polinizador puede visitar. Cada elemento contiene:

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `id` | entero | Identificador único de la flor. |
| `x` | número | Coordenada horizontal dentro del cultivo. |
| `y` | número | Coordenada vertical dentro del cultivo. |
| `tipo` | texto | Variedad de la flor: lavanda, aciano, margarita o rosa. |
| `nectar` | número | Cantidad de néctar disponible en la flor. |
| `color` | texto | Color hexadecimal usado para representar la flor. |

Las coordenadas se encuentran dentro del rectángulo definido por `cultivo.ancho`
y `cultivo.alto`. Por ejemplo, una flor con `"x": 10, "y": 20` está situada a 10
unidades del origen horizontal y a 20 del origen vertical.

### `condiciones`

Agrupa las condiciones que pueden afectar el recorrido.

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `viento.velocidad` | número | Intensidad del viento. |
| `viento.direccion` | texto | Dirección del viento. En el archivo actual es `"NO"`. |
| `temperatura` | número | Temperatura ambiental del cultivo. 
| `humedad` | número | Porcentaje de humedad ambiental.
| `lluvia` | número | Cantidad o intensidad de lluvia.
| `luz` | número | Nivel de iluminación del ambiente.
| `zonas_riesgo` | lista | Zonas circulares que representan áreas peligrosas. |

Cada elemento de `zonas_riesgo` contiene `x`, `y`, `radio` y `descripcion`. El
punto central es (`x`, `y`) y el área de riesgo se considera dentro de la distancia
indicada por `radio`.

### `polinizador`

Define las características del polinizador utilizadas para calcular el recorrido.

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `energia_inicial` | número | Energía disponible al comenzar la ruta. |
| `capacidad_carga` | número | Cantidad máxima de néctar que puede transportar. |
| `velocidad` | número | Velocidad de desplazamiento del polinizador. |
| `energia_minima` | número | Cantidad mínima de energía que debe conservar.
| `consumo_ennergia` | número | Energía consumida durante el desplazamiento, según el modelo de simulación.
| `nectar_actual` | número | Cantidad de néctar que transporta actualmente.
| `radio_detección` | número | Distancia máxima a la que puede detectar flores.
| `resitencia_viento` | número | Capacidad del polinizador para resistir los efectos del viento.
| `posicion_inicial` | objeto | Coordenadas donde comienza el recorrido.

Cada elemento de `posicion_inical` contiene `x`, `y`.

## Códigos HTTP comunes

Significados de códigos estándar que pueden aparecer al usar una API; no implica
que todos estén implementados por este proyecto.

| `400 Bad Request` | Bad Request | La solicitud tiene datos o formato inválidos. |
| `401 Unauthorized` | Unauthorized | Falta autenticación válida para acceder al recurso. |
| `404 Not Found` | Not Found | El recurso solicitado no existe. |
| `405 Method Not Allowed` | Method Not Allowed | El método HTTP no está permitido para ese recurso. |
| `422 Unprocessable Content` | Unprocessable Content | El formato de la solicitud es válido, pero sus instrucciones o datos no se pueden procesar. |
| `429 Too Many Requests` | Too Many Requests | Se enviaron demasiadas solicitudes en un período determinado. |
| `500 Internal Server Error` | Internal Server Error | Ocurrió un error inesperado en el servidor. |
### Error de conexión

No es un código HTTP: ocurre cuando no se logra establecer la conexión con el
servidor, por lo que no se recibe una respuesta HTTP.


## ENPOINTS

## Endpoints de la API

Los endpoints son las direcciones que permiten interactuar con los recursos de la API mediante diferentes métodos HTTP.

### Flores

| `GET` | `/flores` | Obtiene todas las flores del cultivo. |
| `GET` | `/flores/{id}` | Consulta una flor por su identificador. |
| `POST` | `/flores` | Registra una nueva flor. |
| `PUT` | `/flores/{id}` | Actualiza todos los datos de una flor. |
| `PATCH` | `/flores/{id}` | Modifica algunos datos de una flor. |
| `DELETE` | `/flores/{id}` | Elimina una flor. |

### Condiciones ambientales

| `GET` | `/condiciones` | Consulta las condiciones ambientales. |
| `PATCH` | `/condiciones` | Actualiza las condiciones ambientales. |

### Polinizador

| `GET` | `/polinizador` | Consulta las características del polinizador. |
| `PATCH` | `/polinizador` | Actualiza sus características. |

### Cultivo

| `GET` | `/cultivo` | Consulta la información del cultivo. |
| `GET` | `/cultivo/obstaculos` | Consulta los obstáculos del cultivo. |
| `GET` | `/cultivo/zonas-riesgo` | Consulta las zonas de riesgo. |

### Simulación y rutas

| `POST` | `/simulacion/iniciar` | Inicia una simulación. |
| `POST` | `/ruta/calcular` | Calcula la ruta óptima del polinizador. |
| `GET` | `/ruta` | Consulta la última ruta calculada. |
| `GET` | `/simulacion/resultado` | Consulta los resultados de la simulación. |
| `POST` | `/simulacion/reiniciar` | Reinicia la simulación.|



