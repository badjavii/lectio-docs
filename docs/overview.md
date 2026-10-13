# La idea completa

Grabo todas mis clases. El objetivo es que esas grabaciones terminen siendo documentos de estudio buenos de verdad, sin que eso signifique pasar horas transcribiendo y ordenando a mano.

El camino tiene cuatro etapas, y cada una produce algo que la siguiente consume:

```
  grabación         transcripción          nota de clase        documento
  de audio    →     automática      →      en Obsidian    →     de estudio
  (teléfono)        (Colab + GPU)          (un chat)            (un chat)

  .m4a              text/<materia>/        notes-vault/         documents-vault/
                    *.md                   <materia>/*.md       <materia>/uNN-*.md
```

## Por qué cuatro etapas y no una

Se podría intentar ir del audio al documento de estudio de una sola vez. No conviene, por tres razones.

**Cada etapa tiene un costo distinto.** Transcribir es caro en GPU y barato en atención. Escribir una nota es lo inverso. Mezclarlas obliga a pagar los dos costos cada vez que algo sale mal.

**Cada etapa se puede rehacer sola.** Si una nota salió mal, se rehace sin volver a transcribir. Si un documento quedó incompleto, se regenera sin tocar las notas.

**Lo que se pierde en cada paso es distinto.** La transcripción pierde precisión en los términos técnicos. La nota pierde el ruido y gana estructura. El documento pierde la cronología y gana orden temático. Si todo pasa de golpe, no hay forma de saber en qué paso se perdió algo.

## Las cuatro etapas

### 1. Captura

Grabo la clase con el teléfono y le pongo nombre según la convención. El nombre lleva institución, semana, día, materia y fecha, y es lo que permite que todo lo demás funcione sin intervención.

Detalle en [`captura.md`](captura.md).

### 2. Transcripción

Un notebook de Colab corre `faster-whisper` sobre la GPU que Google presta gratis. Entra por semana, sale por materia.

Detalle en [`transcripcion.md`](transcripcion.md).

### 3. Nota de clase

Un chat nuevo, con el prompt, el template y la transcripción. Sale una nota de Obsidian de esa clase, con las explicaciones completadas y separando lo que dijo el profesor de lo que se agregó.

Va a `notes-vault/<materia>/`, con el mismo nombre que la transcripción.

### 4. Documento de estudio

Un chat nuevo, con el prompt, el template, las notas de la materia, los recursos del profesor y el registro. Salen uno o varios documentos organizados por unidad temática, más el registro actualizado.

Va a `documents-vault/<materia-larga>/`.

## El registro

Es la pieza que hace que la etapa 4 funcione entre chats distintos.

Un chat no recuerda el anterior. Sin algo que lleve el estado, cada vez que genero documentos de una materia el modelo tendría que deducir desde cero qué se hizo antes, y se equivocaría: duplicaría contenido o saltearía clases.

El registro es un archivo por materia, dentro del vault de documentos, que lleva:

- qué unidades existen y de qué trata cada una,
- **de qué notas salió cada documento**,
- qué notas todavía no se incorporaron.

Con eso, un chat nuevo sabe exactamente dónde retomar. Es append-only: se agrega, no se reescribe, salvo aprobación explícita.

## Los tres repositorios

| Repo | Qué tiene |
|---|---|
| **este** | Documentación, prompts, templates, ejemplos y el notebook |
| `notes-vault` | Vault de Obsidian con las notas de clase, por materia |
| `documents-vault` | Vault de Obsidian con los documentos de estudio y los registros |

Los vaults están separados a propósito. Son dos formas distintas de mirar lo mismo: las notas siguen la cronología de las clases, los documentos siguen la estructura de la materia. Mezclarlos en un solo vault haría que el grafo de Obsidian mezcle dos criterios y deje de ser legible.

El costo de separarlos es que los enlaces no cruzan de un vault al otro. Es aceptable: cada vault se navega solo, y la trazabilidad entre documento y notas la da el registro, no los enlaces.
