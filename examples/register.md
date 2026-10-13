<!--
EJEMPLO ILUSTRATIVO. Un registro ya poblado, después de dos corridas.
El registro en blanco está en `templates/register.md`.
-->

---
materia: "apis-python"
codigo: "apispy"
actualizado: 2026-10-12
documentos: 3
notas_incorporadas: 4
---

# Registro — Desarrollo de APIs en Python

> [!important] Reglas de este archivo
> Este archivo es el **estado** de la generación de documentos de estudio de esta materia. Viaja de un chat a otro para recuperar el contexto.
>
> 1. **Es append-only.** Se agregan entradas y se completan las listas de notas incorporadas. **No se reescriben ni se borran entradas existentes.**
> 2. **Para modificar una entrada ya escrita hace falta aprobación explícita del Admin.** Si creés que una entrada está mal, decilo y esperá respuesta; no la corrijas por tu cuenta.
> 3. **Los números de unidad son estables.** Una vez que `u02` es un tema, lo sigue siendo. Si aparece material que "debería" ir antes, se crea una unidad nueva con el número que sigue, no se renumera.
> 4. **Si este archivo está vacío de documentos**, es la primera corrida de esta materia: hay que analizar todas las notas, decidir las unidades y crear este registro completo.

## Documentos

### u00-introduction
**Título:** Qué es una API REST y dónde encaja FastAPI
**Archivo:** `u00-introduction.md`
**Resumen:** Repaso de los conceptos de REST que la materia da por sabidos, y ubicación de FastAPI frente a Flask. Es la unidad de contexto: no introduce nada que se evalúe por sí solo, pero las demás lo asumen.
**Notas incorporadas:**
- `ucab-w1-d4-apispy-17-09-2026`
**Recursos usados:**
- `programa-de-la-materia.pdf`

### u01-fastapi-basics
**Título:** Primera API con FastAPI
**Archivo:** `u01-fastapi-basics.md`
**Resumen:** La aplicación mínima, el decorador de ruta, el orden de declaración de rutas y la distinción entre path y query parameters. Incluye la advertencia del profesor sobre el orden, marcada para el examen.
**Notas incorporadas:**
- `ucab-w2-d4-apispy-24-09-2026`
**Recursos usados:**
- (ninguno)

### u02-pydantic
**Título:** Validación con Pydantic
**Archivo:** `u02-pydantic.md`
**Resumen:** Modelos, tipos y validación automática del cuerpo de las peticiones. Se apoya en u01 para los endpoints.
**Notas incorporadas:**
- `ucab-w3-d4-apispy-01-10-2026`
- `ucab-w4-d4-apispy-08-10-2026`
**Recursos usados:**
- `laminas-pydantic.pdf`
- `foto-pizarron-08-10.jpg`

## Notas sin incorporar

- `ucab-w5-d4-apispy-15-10-2026` — trata de Docker, que no corresponde a ninguna unidad existente. No se abrió unidad nueva porque con una sola clase el documento quedaría muy pobre; conviene esperar la próxima.

## Historial

| Fecha | Qué se hizo |
|---|---|
| 2026-10-05 | Primera corrida. Se identificaron u00, u01 y u02. Se escribieron u00 y u01. |
| 2026-10-12 | Se incorporaron dos notas a u02 y se escribió el documento. Queda pendiente la clase de Docker. |
