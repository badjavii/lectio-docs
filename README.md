<div align="center">

# Lectio

_De la grabación de una clase a un documento de estudio_

[![Transcripción](https://img.shields.io/badge/Transcripci%C3%B3n-faster--whisper-94e2d5?labelColor=181825&style=for-the-badge&logo=python&logoColor=white)](https://github.com/SYSTRAN/faster-whisper)
[![Entorno](https://img.shields.io/badge/Entorno-Google%20Colab-fab387?labelColor=181825&style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![Notas](https://img.shields.io/badge/Notas-Obsidian-cba6f7?labelColor=181825&style=for-the-badge&logo=obsidian&logoColor=white)](https://obsidian.md/)
[![License](https://img.shields.io/github/license/Badjavii/lectio?color=a6e3a1&labelColor=181825&style=for-the-badge)](https://github.com/Badjavii/lectio/blob/main/LICENSE)

</div>

## Sobre este proyecto

Lectio es el sistema con el que convierto las grabaciones de mis clases universitarias en documentos de estudio. Grabo cada clase con el teléfono, un notebook las transcribe sobre la GPU que Google presta gratis, y a partir de esas transcripciones genero notas de clase y después documentos organizados por tema.

**Este repositorio no contiene notas ni documentos.** Contiene las instrucciones para producirlos: la documentación del proceso, los prompts que se le pasan a la IA, las plantillas que definen la forma de cada resultado y los ejemplos de cómo se ve cada cosa cuando está bien hecha.

Las notas y los documentos viven en dos vaults de Obsidian aparte.

## El flujo

```
  grabación         transcripción          nota de clase        documento
  de audio    →     automática      →      en Obsidian    →     de estudio
  (teléfono)        (Colab + GPU)          (un chat)            (un chat)
```

Las dos primeras etapas están automatizadas. Las dos últimas se hacen abriendo un chat y pasándole los archivos que correspondan.

Son cuatro etapas y no una porque cada una tiene un costo distinto (transcribir es caro en GPU y barato en atención, escribir una nota es lo inverso) y porque cada una se puede rehacer sola. Si una nota salió mal, se rehace sin volver a transcribir.

## Qué hay en este repositorio

```
docs/           la idea, el uso, las convenciones y las decisiones
prompts/        lo que se le pega al chat para generar notas y documentos
templates/      la forma que tiene que tener cada resultado
subjects/       una ficha por materia: nombres, stack, vocabulario técnico
examples/       cómo se ve cada cosa cuando está bien hecha
tools/          el notebook de Colab que transcribe
```

| Si querés… | Leé |
|---|---|
| entender la idea completa | [`docs/overview.md`](docs/overview.md) |
| usarlo: qué pasar a cada chat | [`docs/uso.md`](docs/uso.md) |
| saber cómo se nombra cada cosa | [`docs/conventions.md`](docs/conventions.md) |
| entender por qué algo es así | [`docs/decisions.md`](docs/decisions.md) |

## Transcripción

El notebook [`tools/transcriptioner.ipynb`](tools/transcriptioner.ipynb) corre
`faster-whisper` sobre una GPU de Colab. Entra por semana, sale por materia.

```
audios/week_2/ucab-w2-d4-apispy-24-09-2026.m4a
        ↓
text/apispy/ucab-w2-d4-apispy-24-09-2026.md
```

Transcribir una clase de dos horas en una CPU de escritorio toma unas nueve horas. Sobre una T4 baja a minutos, y esa diferencia es la razón de que el procesamiento viva en Colab y no localmente.

Detalles de uso y errores conocidos en [`docs/transcripcion.md`](docs/transcripcion.md).

## Las dos operaciones con IA

### Generar una nota de clase

Chat nuevo. Se le pasa:

| Archivo | De dónde sale |
|---|---|
| [`prompts/generate-note.md`](prompts/generate-note.md) | este repo — pegado como primer mensaje |
| [`templates/note.md`](templates/note.md) | este repo — adjunto |
| `subjects/<codigo>.md` | este repo — adjunto |
| la transcripción | Drive, `text/<materia>/` |

El resultado es una nota de esa clase, con las explicaciones completadas hasta que se entiendan sin haber estado ahí. Va a `lectio-notes/<materia>/` con el mismo nombre que la transcripción.

**La regla central del prompt** es separar lo que dijo el profesor de lo que agrega el modelo, usando callouts distintos. El motivo es práctico: en un examen se evalúa lo que se dio en clase, no lo que es cierto en general. La segunda regla es no completar lo que no se entendió; si el audio se cortó, la nota lo dice en lugar de inventar.

### Generar documentos de estudio

Chat nuevo. Se le pasa:

| Archivo | De dónde sale |
|---|---|
| [`prompts/generate-study-document.md`](prompts/generate-study-document.md) | este repo (pegado como primer mensaje) |
| [`templates/study-document.md`](templates/study-document.md) | este repo (adjunto) |
| `subjects/<codigo>.md` | este repo (adjunto) |
| `register.md` de la materia | `lectio-docs/<materia-larga>/` |
| las notas de la materia | `lectio-notes/<materia>/` |
| PDFs del profesor, fotos del pizarrón | donde los tengas |

El resultado son uno o varios documentos organizados por unidad temática (`u00-introduction.md`, `u01-docker.md`) más el registro actualizado.

## El registro

Es la pieza que hace que la segunda operación funcione entre chats distintos.

Un chat no recuerda el anterior. Sin algo que lleve el estado, cada vez que genero documentos de una materia el modelo tendría que deducir desde cero qué se hizo antes, y se equivocaría: duplicaría contenido o saltearía clases.

El registro es un archivo por materia, dentro del vault de documentos, que lleva qué unidades existen, **de qué notas salió cada documento** y qué notas todavía no se incorporaron. Con eso, un chat nuevo sabe exactamente dónde retomar.

Es append-only: se agrega, no se reescribe, salvo aprobación explícita.

## Los tres repositorios

| Repo | Qué tiene |
|---|---|
| **lectio** (este) | documentación, prompts, plantillas, ejemplos y el notebook |
| **lectio-notes** | vault de Obsidian: una nota por clase, organizada por materia |
| **lectio-docs** | vault de Obsidian: documentos por unidad temática, más el registro de cada materia |

Los vaults están separados a propósito. Son dos formas de mirar lo mismo con criterios incompatibles: las notas siguen la cronología de las clases, los documentos siguen la estructura temática de la materia. En un solo vault, el grafo de Obsidian mezclaría ambos criterios y dejaría de ser legible.

El costo es que los wikilinks no cruzan de un vault al otro. Es aceptable: la trazabilidad entre un documento y sus notas la da el registro, no los enlaces.

## Convenciones

El nombre de archivo es lo que hace funcionar todo lo demás sin intervención:

```
ucab-w2-d4-apispy-24-09-2026.m4a
│    │  │  │      └─ fecha de la clase, DD-MM-YYYY
│    │  │  └──────── código de la materia
│    │  └─────────── día de la semana, 1 = lunes … 7 = domingo
│    └────────────── semana del semestre
└─────────────────── institución
```

El guion separa campos, así que ningún campo lleva guiones: la materia va toda junta (`ciberofflab`, no `ciberoff-lab`). El mismo nombre, cambiando la extensión, viaja del audio a la transcripción y de ahí a la nota.

La fecha es referencia para el lector; `w#` y `d#` son los que clasifican. Por eso no hace falta declarar en ningún lado cuándo empezó el semestre.

El contrato completo está en [`docs/conventions.md`](docs/conventions.md).

## Estado

| Etapa | Estado |
|---|---|
| Captura | funcionando, con renombrado manual o Tasker |
| Transcripción | funcionando |
| Notas de clase | prompts y plantillas listos, sin uso real todavía |
| Documentos de estudio | prompts y plantillas listos, sin uso real todavía |

## Créditos

Este proyecto está orgullosamente diseñado y desarrollado por **Badjavii**, desarrollador junior.
