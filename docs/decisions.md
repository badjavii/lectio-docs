# Decisiones

Qué se decidió, y sobre todo **por qué**. Append-only: se agregan entradas, no se reescriben.

El motivo de este archivo es práctico. Varias de estas decisiones parecen mejorables a primera vista, y sin el motivo escrito se vuelven a discutir cada vez. O peor, una IA propone "mejorarlas" y se rompen cosas que ya funcionan.

---

## 001 - La semana sale del nombre, no de la fecha

**Decisión.** `w#` y `d#` del nombre de archivo deciden la clasificación. La fecha queda como dato de referencia.

**Por qué.** Deducir la semana de la fecha obligaría a declarar cuándo empezó el semestre y a mantener esa referencia correcta todo el período. La semana ya está escrita en el nombre y en la carpeta: deducirla sería recalcular algo que ya está dicho dos veces, con una fuente más que puede estar mal.

**Consecuencia.** No existe `SEMESTRE_INICIO` en ningún lado.

---

## 002 - La materia no lleva guiones

**Decisión.** `ciberofflab`, no `ciberoff-lab`.

**Por qué.** El guion es el separador de campos del nombre. Si la materia puede llevar guiones, el patrón deja de ser exacto: un nombre mal formado como `ucab-w2-d4-apispy-lab-24-09-2026` se interpretaría como una materia llamada `apispy-lab` y crearía una carpeta que parece legítima.

Con la materia sin guiones, ese nombre simplemente no coincide y va a `_sin_materia` con un aviso. Lo mal formado se vuelve visible en vez de disfrazarse.

---

## 003 - Entrada por semana, salida por materia

**Decisión.** Los audios se organizan en `audios/week_N/`; las transcripciones en `text/<materia>/`.

**Por qué.** Cada criterio responde a un uso distinto. Los audios entran por semana porque así se graban y se suben: al terminar la semana hay un lote que procesar, y la carpeta acota ese lote. Las transcripciones salen por materia porque así se estudian: al preparar un parcial no importa de qué semana fue cada clase.

El nombre de archivo conecta las dos vistas, porque lleva semana y materia.

---

## 004 - El procesamiento corre en Colab, no local

**Decisión.** La transcripción se hace en un notebook de Google Colab.

**Por qué.** Medición real: `medium` con `int8` en la CPU de escritorio da ~0.23x realtime, o sea unas nueve horas para una clase de dos. Sobre una T4 el mismo trabajo baja a minutos.

**Consecuencia.** Existe una app de terminal (`oido`) que hace lo mismo localmente y funciona, pero quedó fuera del flujo real. No se mantiene.

---

## 005 - PyAV fijado por debajo de la versión 19

**Decisión.** El notebook instala `av<19`.

**Por qué.** PyAV 19 eliminó el parámetro `metadata_errors` de `av.open()`, y `faster-whisper` todavía se lo pasa al decodificar. Sin la restricción, la instalación funciona, el modelo se construye, y recién al transcribir el primer archivo aparece `TypeError: open() got an unexpected keyword argument 'metadata_errors'` — con todos los archivos fallando uno tras otro.

Verificado: av 19.0.1 reproduce el error, av 18.1.0 no.

---

## 006 - Dos vaults separados, sin enlaces entre ellos

**Decisión.** `notes-vault` y `documents-vault` son vaults de Obsidian distintos.

**Por qué.** Son dos formas de mirar lo mismo con criterios incompatibles: las notas siguen la cronología de las clases, los documentos siguen la estructura temática de la materia. En un solo vault, el grafo mezcla ambos criterios y deja de ser legible.

**Costo aceptado.** Los wikilinks no cruzan vaults. La trazabilidad entre un documento y las notas de las que salió la da el registro, no los enlaces.

---

## 007 - El registro lleva qué notas alimentaron cada documento

**Decisión.** Cada entrada del registro lista las notas incorporadas, y hay una sección de notas sin incorporar.

**Por qué.** El registro existe para que un chat nuevo recupere el contexto. Si solo tuviera índice y resumen, al llegar las notas de la semana siguiente el chat tendría que deducir cuáles ya están incorporadas leyendo los resúmenes. Esa inferencia falla, y cuando falla duplica contenido o saltea una clase.

Con la lista explícita, saber dónde retomar es determinístico.

---

## 008 - Los números de unidad son estables

**Decisión.** Una vez que `u02` es un tema, lo sigue siendo. El material que conceptualmente iría antes se agrega como unidad nueva al final.

**Por qué.** Renumerar cambia los nombres de archivo, y con eso rompe los wikilinks del vault y las referencias del registro. El orden conceptual se expresa en el "Mapa de la unidad" de cada documento, no en la numeración.

---

## 009 - El registro es append-only

**Decisión.** Se agregan entradas y se completan listas. Modificar una entrada existente requiere aprobación explícita del Admin.

**Por qué.** Cada generación ocurre en un chat distinto, con un modelo que no vio los anteriores. Sin esta regla, cada corrida reescribiría la historia según su propio criterio, y el registro dejaría de ser un estado confiable para pasar a ser la opinión del último chat que lo tocó.

---

## 010 - Las notas separan lo que dijo el profesor de lo agregado

**Decisión.** El contenido de clase va en el cuerpo; lo agregado para claridad va en callouts `> [!tip]`; las formulaciones textuales que importan van en `> [!quote]`.

**Por qué.** En un examen se evalúa lo que se dio en clase, no lo que es cierto en general. Una nota que mezcla ambas cosas deja de servir para estudiar, porque no hay forma de saber qué parte es la que el profesor va a preguntar.
