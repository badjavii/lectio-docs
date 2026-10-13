<!--
EJEMPLO ILUSTRATIVO. Es la nota que saldría de `examples/transcription.md`.
Compará los dos archivos para ver qué hace el prompt: ordena, completa las explicaciones, corrige los términos y marca lo que no se entendió.
-->

---
materia: "apispy"
semana: 2
dia_semana: 4
fecha: 2026-09-24
fuente: "ucab-w2-d4-apispy-24-09-2026.md"
tags:
  - clase
  - apispy
  - fastapi
---

# Introducción a FastAPI: primera API y parámetros

> [!abstract] En una línea
> Qué aporta FastAPI sobre Flask, cómo se escribe el endpoint mínimo, y la diferencia entre path parameters y query parameters.

## Lo que se vio

- Qué distingue a [[FastAPI]] de [[Flask]]
- La aplicación mínima: instancia y decorador de ruta
- El orden de las rutas y por qué importa
- Path parameters contra query parameters

---

## Qué aporta FastAPI sobre Flask

La clase asume que ya se sabe construir una API con Flask. FastAPI cubre el mismo terreno, con dos agregados:

**Validación automática.** Se declara el tipo de dato esperado y el framework verifica que lo que llega lo cumpla, sin escribir esa comprobación a mano. Lo hace apoyándose en [[Pydantic]], que es el tema de la clase siguiente.

**Documentación generada sola.** Al levantar el servidor, la documentación interactiva queda disponible en `/docs` sin configurarla.

## La aplicación mínima

Se importa `FastAPI`, se crea la instancia y se decora la función que atiende la ruta:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items")
def listar_items():
    return {"items": []}
```

> [!tip] Agregado para claridad
> El profesor recordó que un decorador es "eso que va con arroba arriba de la función". En concreto: `@app.get("/items")` registra la función como manejadora de las peticiones GET a esa ruta, sin modificar la función en sí.

## El orden de las rutas importa

Cuando dos rutas pueden coincidir con la misma URL, **gana la que se definió primero**. Si una ruta fija como `/items/algo` se declara antes que una con parámetro como `/items/{id}`, la fija intercepta las peticiones que iban a la otra.

> [!quote] Lo que dijo el profesor
> "Esto va para el examen, acuérdense, el orden importa."

> [!warning] Dudoso en la transcripción
> En la explicación del orden de rutas hay un tramo marcado como inaudible. Por el contexto se entiende que el framework toma la primera coincidencia, pero conviene confirmar el ejemplo exacto que dio.

## Path parameters y query parameters

| | Dónde van | Obligatorios |
|---|---|---|
| **Path parameters** | en la ruta: `/items/{id}` | sí, forman parte de la URL |
| **Query parameters** | después del `?`: `/items?limit=10` | no, admiten valor por defecto |

> [!tip] Agregado para claridad
> La obligatoriedad de los path parameters no es una regla del framework sino una consecuencia: sin ese segmento, la URL no coincide con la ruta.

## Para el examen

- **El orden de declaración de las rutas**, marcado explícitamente por el profesor.

## Pendientes

- **Cómo se ejecuta el servidor.** El profesor empezó a explicarlo (aclaró que no se corre con `python archivo.py`) pero el audio se corta justo ahí. Solo se alcanza a oír que se usa una opción de recarga automática al guardar.
- **Lectura asignada**: la sección *First Steps* de la documentación de FastAPI.
- **Próxima clase**: Pydantic en profundidad.
