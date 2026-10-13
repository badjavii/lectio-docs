<!--
EJEMPLO ILUSTRATIVO. El documento `u01-fastapi-basics.md` del ejemplo de
registro. Está recortado: un documento real es bastante más largo, porque
integra varias clases.
-->

---
materia: "apis-python"
codigo: "apispy"
unidad: "u01-fastapi-basics"
titulo: "Primera API con FastAPI"
notas_fuente:
  - "ucab-w2-d4-apispy-24-09-2026"
recursos: []
actualizado: 2026-10-05
tags:
  - documento-estudio
  - apispy
---

# Primera API con FastAPI

> [!abstract] De qué trata esta unidad
> Cómo se construye el endpoint más simple posible con FastAPI y cómo se reciben datos del cliente. Al terminar deberías poder escribir una API de lectura con rutas parametrizadas, y saber por qué el orden en que las declarás cambia el comportamiento.

## Mapa de la unidad

1. **La aplicación mínima**: instancia y decorador. Sin esto no hay nada.
2. **Rutas y su orden**: la regla que más errores causa.
3. **Parámetros**: cómo entran los datos del cliente.

Se asume [[u00-introduction]], en particular la noción de método HTTP.

---

## La aplicación mínima

Una API de FastAPI son tres cosas: la importación, la instancia y al menos una función decorada.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items")
def listar_items():
    return {"items": []}
```

El decorador `@app.get("/items")` asocia la función con las peticiones GET a esa ruta. La función en sí no cambia: el decorador la registra en la aplicación.

> [!tip] Agregado para claridad
> El valor de retorno se serializa a JSON automáticamente. Devolver un `dict` alcanza; no hace falta llamar a nada que lo convierta.

## Rutas y su orden

Cuando dos rutas pueden coincidir con la misma URL, **gana la primera declarada**.

```python
@app.get("/items/especiales")   # esta intercepta
def especiales(): ...

@app.get("/items/{item_id}")    # esta nunca ve "especiales"
def obtener(item_id: int): ...
```

Invertido el orden, la ruta con parámetro captura también `/items/especiales` e intenta convertir `"especiales"` a entero.

> [!warning] Error común
> Marcado explícitamente por el profesor como material de examen. La regla es declarar siempre las rutas fijas antes que las parametrizadas.

## Parámetros

| | Dónde van | Obligatorios | Ejemplo |
|---|---|---|---|
| **Path** | en la ruta | sí | `/items/42` |
| **Query** | después del `?` | no | `/items?limit=10` |

Los path parameters son obligatorios porque sin ellos la URL no coincide con la ruta. Los query parameters admiten valor por defecto, y ese default es lo que los vuelve opcionales.

---

## Síntesis

- Tres elementos: importar, instanciar, decorar.
- Las rutas fijas van antes que las parametrizadas.
- Path parameter = obligatorio, está en la ruta. Query parameter = opcional, va después del `?`.

## Preguntas de autoevaluación

> [!question]- ¿Por qué `/items/especiales` deja de funcionar si se declara después de `/items/{item_id}`?
> Porque FastAPI resuelve con la primera ruta que coincide. La parametrizada coincide con cualquier segmento, incluido `"especiales"`, e intenta convertirlo al tipo declarado.

> [!question]- ¿Qué vuelve opcional a un query parameter?
> Tener un valor por defecto en la firma de la función.

## Origen de este documento

| Clase | Fecha | Qué aportó |
|---|---|---|
| `ucab-w2-d4-apispy-24-09-2026` | 2026-09-24 | Todo el contenido de la unidad |

## Vacíos conocidos

- **Cómo se ejecuta el servidor.** La nota de origen lo marca como pendiente: el audio se corta cuando el profesor lo estaba explicando. Falta confirmar el comando y la opción de recarga automática.
- **Métodos distintos de GET.** La unidad solo cubre lectura. POST, PUT y DELETE no aparecieron todavía en ninguna clase.
