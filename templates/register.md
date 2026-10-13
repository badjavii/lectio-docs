---
materia: "{{nombre-largo-materia}}"
codigo: "{{codigo-materia}}"
actualizado: {{YYYY-MM-DD}}
documentos: 0
notas_incorporadas: 0
---

# Registro — {{nombre-largo-materia}}

> [!important] Reglas de este archivo
> Este archivo es el **estado** de la generación de documentos de estudio de esta materia. Viaja de un chat a otro para recuperar el contexto.
>
> 1. **Es append-only.** Se agregan entradas y se completan las listas de notas incorporadas. **No se reescriben ni se borran entradas existentes.**
> 2. **Para modificar una entrada ya escrita hace falta aprobación explícita del Admin.** Si creés que una entrada está mal, decilo y esperá respuesta; no la corrijas por tu cuenta.
> 3. **Los números de unidad son estables.** Una vez que `u02` es un tema, lo sigue siendo. Si aparece material que "debería" ir antes, se crea una unidad nueva con el número que sigue, no se renumera.
> 4. **Si este archivo está vacío de documentos**, es la primera corrida de esta materia: hay que analizar todas las notas, decidir las unidades y crear este registro completo.

## Documentos

<!--
Una entrada por documento de estudio. El orden es por número de unidad.
Formato de cada entrada:

### uNN-slug
**Título:** {{título legible}}
**Archivo:** `uNN-slug.md`
**Resumen:** {{dos o tres oraciones sobre qué cubre el documento}}
**Notas incorporadas:**
- `{{nombre-de-nota}}`
**Recursos usados:**
- `{{archivo.pdf}}`
-->

{{Sin documentos todavía.}}

## Notas sin incorporar

<!--
Las notas de esta materia que todavía no entraron a ningún documento. Al incorporar una nota, se mueve de acá a la lista de su documento.
-->

{{Ninguna registrada todavía.}}

## Historial

<!--
Una línea por corrida. Permite saber qué pasó la última vez sin leer todo.
-->

| Fecha | Qué se hizo |
|---|---|
