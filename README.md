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

## Uso del archivo

Mantener el nombre y las claves principales (`flores`, `condiciones`, `polinizador`
y `cultivo`) permite que otros programas puedan interpretar el archivo.

Desde JavaScript, los datos se pueden cargar mediante una petición HTTP:

```javascript
fetch("cultivo.json")
  .then((respuesta) => {
    if (!respuesta.ok) {
      throw new Error(`No se pudo cargar el JSON: ${respuesta.status}`);
    }
    return respuesta.json();
  })
  .then((datos) => {
    console.log(datos.cultivo);
    console.log(datos.flores);
  })
  .catch((error) => console.error(error));
```

Desde Python:

```python
import json

with open("cultivo.json", "r", encoding="utf-8") as archivo:
    datos = json.load(archivo)

print(datos["cultivo"]["nombre"])
print(datos["polinizador"]["energia_inicial"])
```

Para probarlo en un navegador, desde la raíz del proyecto ejecuta:

```bash
python3 -m http.server 8000
```

Después abre `http://localhost:8000`. El código JavaScript debe hacerse desde el
servidor, ya que cargar `cultivo.json` directamente con `fetch` desde `file://`
puede bloquearse por las políticas de seguridad del navegador.
