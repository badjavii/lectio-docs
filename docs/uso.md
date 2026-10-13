# Uso

Qué se hace, cuándo, y qué archivos se pasan a cada chat.

## Durante la semana

Grabar cada clase y nombrarla según la convención:

```
ucab-w2-d4-apispy-24-09-2026.m4a
```

Subirla a `audios/week_N/` en Drive. Ver [`captura.md`](captura.md).

## Fin de semana — transcribir

1. Abrir `tools/transcriptioner.ipynb` en Colab.
2. `Entorno de ejecución → Cambiar tipo de entorno → GPU`.
3. Ejecutar las secciones 1 y 2.
4. En la sección 3, poner `SEMANAS = []` para procesar todo lo pendiente.
5. Ejecutar de la 3 a la 6.

Las transcripciones quedan en `text/<materia>/` en Drive.

## Por cada clase — generar la nota

**Chat nuevo.** Se le pasa:

| Archivo | De dónde sale |
|---|---|
| `prompts/generate-note.md` | este repo — pegado como primer mensaje |
| `templates/note.md` | este repo — adjunto |
| `subjects/<codigo>.md` | este repo — adjunto |
| la transcripción | Drive, `text/<materia>/` |

**Resultado**: una nota de clase. Guardarla en `notes-vault/<materia>/` con el
mismo nombre que la transcripción.

> [!tip]
> Un chat por clase. Si se procesan varias clases en el mismo chat, el modelo
> arrastra contexto de la anterior y empieza a mezclar.

## Cuando hay varias notas — generar documentos de estudio

**Chat nuevo.** Se le pasa:

| Archivo | De dónde sale |
|---|---|
| `prompts/generate-study-document.md` | este repo — pegado como primer mensaje |
| `templates/study-document.md` | este repo — adjunto |
| `subjects/<codigo>.md` | este repo — adjunto |
| `register.md` de la materia | `documents-vault/<materia-larga>/` |
| las notas de la materia | `notes-vault/<materia>/` |
| PDFs, fotos del pizarrón | donde los tengas |

La primera vez, el registro va en blanco: se copia `templates/register.md` a `documents-vault/<materia-larga>/register.md` y se completan los datos de la cabecera.

**Resultado**: uno o varios documentos (`uNN-slug.md`) y el registro actualizado. Los dos van a `documents-vault/<materia-larga>/`.

## Cada cuánto conviene generar documentos

No después de cada clase. Un documento de estudio integra varias clases sobre un mismo tema, así que generarlo con una sola nota produce un documento pobre que después hay que extender igual.

Lo razonable es cuando se cierra un tema (el profesor pasa a otra cosa) o cada tres o cuatro clases.

## Mantenimiento

**La ficha de materia se actualiza sola, con el uso.** Cada vez que una nota sale con un término mal transcrito, se agrega a la tabla de `subjects/<codigo>.md`. La próxima nota ya sale bien.

**Las decisiones se anotan.** Si durante el uso se decide algo que cambia cómo funciona el flujo, va a [`decisions.md`](decisions.md) con su motivo. Es lo que evita volver a discutir lo mismo en tres meses.
