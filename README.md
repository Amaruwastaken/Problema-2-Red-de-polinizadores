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

## Códigos HTTP comunes

Significados de códigos estándar que pueden aparecer al usar una API; no implica
que todos estén implementados por este proyecto.

| Código | Nombre estándar | Significado |
| --- | --- | --- |
| `200 OK` | OK | La solicitud se procesó correctamente. |
| `201 Created` | Created | La solicitud se completó y creó un recurso. |
| `202 Accepted` | Accepted | La solicitud fue recibida y aceptada para su procesamiento, pero aún no se completó. |
| `400 Bad Request` | Bad Request | La solicitud tiene datos o formato inválidos. |
| `401 Unauthorized` | Unauthorized | Falta autenticación válida para acceder al recurso. |
| `403 Forbidden` | Forbidden | El servidor entendió la solicitud, pero deniega el acceso. |
| `404 Not Found` | Not Found | El recurso solicitado no existe. |
| `405 Method Not Allowed` | Method Not Allowed | El método HTTP no está permitido para ese recurso. |
| `409 Conflict` | Conflict | La solicitud entra en conflicto con el estado actual del recurso. |
| `418 I'm a teapot` | I'm a teapot | Código de la RFC 2324; indica que el servidor rechaza preparar café porque es una tetera. |
| `422 Unprocessable Content` | Unprocessable Content | El formato de la solicitud es válido, pero sus instrucciones o datos no se pueden procesar. |
| `429 Too Many Requests` | Too Many Requests | Se enviaron demasiadas solicitudes en un período determinado. |
| `500 Internal Server Error` | Internal Server Error | Ocurrió un error inesperado en el servidor. |
| `502 Bad Gateway` | Bad Gateway | Un servidor que actúa como intermediario recibió una respuesta inválida del servidor ascendente. |
| `503 Service Unavailable` | Service Unavailable | El servicio no está disponible temporalmente. |
| `504 Gateway Timeout` | Gateway Timeout | Un servidor intermediario no recibió a tiempo una respuesta del servidor ascendente. |

### Error de conexión

No es un código HTTP: ocurre cuando no se logra establecer la conexión con el
servidor, por lo que no se recibe una respuesta HTTP.
