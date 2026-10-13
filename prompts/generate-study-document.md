# Prompt — Generar documentos de estudio

> Copiá todo lo que está debajo de la línea y pegalo como primer mensaje de un chat nuevo. Adjuntá además: el template del documento, el template o el archivo del registro, la ficha de la materia, las notas de clase y los recursos extra (PDFs del profesor, fotos del pizarrón).

---

Vas a generar documentos de estudio a partir de notas de clase de una materia universitaria, y a mantener un registro del estado de ese trabajo.

## Lo que te estoy pasando

1. **El template del documento** (`study-document.md`) — la estructura del resultado.
2. **El registro de la materia** (`register.md`) — el estado del trabajo hecho hasta ahora. **Leelo primero.**
3. **La ficha de la materia** (`subjects/<codigo>.md`).
4. **Las notas de clase** — una por clase, ya procesadas.
5. **Recursos adicionales**, si los hay: PDFs del profesor, fotos del pizarrón o de las láminas.

## Antes de escribir nada: leé el registro

El registro determina en cuál de los dos modos estás.

### Modo A — el registro está vacío

Si la sección "Documentos" dice que no hay documentos, es la primera vez que se trabaja esta materia. Entonces:

1. **Leé todas las notas** y determiná qué unidades temáticas hay. Una unidad agrupa un tema coherente, que puede abarcar varias clases o solo parte de una. **No es una unidad por clase**: el criterio es el tema, no la fecha.
2. **Numerá las unidades** en orden de dependencia conceptual, empezando en `u00`: qué hay que entender primero para entender lo siguiente. Puede no coincidir con el orden cronológico.
3. **Nombrá cada unidad** `uNN-slug`, con el slug en minúsculas y con guiones: `u00-introduction`, `u01-docker`, `u02-fastapi`.
4. **Escribí los documentos** que tengan material suficiente.
5. **Creá el registro completo** con todas las unidades que identificaste, incluidas las que todavía no tienen material suficiente para un documento.

### Modo B — el registro ya tiene documentos

Ya se trabajó antes. Entonces:

1. **Mirá qué notas están en "Notas sin incorporar"** y cuáles no figuran en ninguna lista. Esas son las nuevas.
2. **Para cada nota nueva, decidí** si extiende una unidad que ya existe o si abre una unidad nueva.
3. **Si extiende una existente**: agregás el contenido al documento de esa unidad y sumás la nota a su lista de notas incorporadas.
4. **Si abre una nueva**: creás la unidad con **el número que sigue al más alto que exista**, aunque el tema conceptualmente vaya antes.
5. **Actualizás el registro** agregando, nunca reescribiendo.

## Reglas del registro

**Los números de unidad son estables.** Una vez que `u02` es FastAPI, lo sigue siendo para siempre. Si aparece material que debería ir antes, va como unidad nueva al final. Renumerar rompe los nombres de archivo y los enlaces del vault.

**El registro es append-only.** Agregás entradas y completás listas. **No reescribís ni borrás lo que ya está.**

**Para modificar una entrada existente necesitás aprobación.** Si encontrás que una entrada está mal (un resumen equivocado, una nota atribuida a la unidad incorrecta) **decímelo y esperá mi respuesta**. No lo corrijas por tu cuenta. Yo soy el Admin.

**Toda nota tiene que quedar contabilizada.** Al terminar, cada nota que te pasé está o en la lista de notas incorporadas de algún documento, o en "Notas sin incorporar" con el motivo. Ninguna puede desaparecer sin dejar rastro.

## Reglas de los documentos

**Un documento de estudio no es una nota de clase larga.** La nota sigue el orden en que el profesor dio las cosas; el documento sigue el orden en que conviene aprenderlas. Integrá lo de varias clases, reordená por lógica del tema, y eliminá las repeticiones.

**Distinguí el origen del contenido**, igual que en las notas: lo que se dio en clase va en el cuerpo; lo que agregás para completar va en callouts `> [!tip]`. Lo que sale del material del profesor (PDFs, láminas) se señala como tal.

**Los vacíos se declaran.** Si una unidad tiene partes que las notas no cubren, la sección "Vacíos conocidos" los enumera. Es la sección que me dice qué clase me conviene volver a escuchar o qué preguntarle al profesor.

**Enlaces de Obsidian**: podés enlazar entre documentos de esta misma materia (`[[u01-docker]]`), porque sabés qué unidades existen, están en el registro.  Conceptos también (`[[contenedor]]`). No enlaces a las notas de clase: están en otro vault y el enlace no resuelve.

## El resultado

1. **Los documentos** que escribiste o extendiste, cada uno completo y con su nombre de archivo (`uNN-slug.md`).
2. **El registro actualizado**, completo, listo para reemplazar al anterior.
3. **Un resumen de la corrida**: qué unidades tocaste, qué notas incorporaste, qué quedó pendiente y por qué.

Si algo del registro te parece mal, o si una nota no encaja en ninguna unidad y no estás seguro de abrir una nueva, **preguntá antes de decidir**.
