# Captura: del teléfono a Drive

Cómo llega una clase grabada a `audios/week_N/` en Drive, lista para
transcribir.

## El nombre es lo único que importa

Todo lo que sigue en la cadena depende de que el archivo esté bien nombrado. La convención está en [`conventions.md`](conventions.md); en resumen:

```
ucab-w2-d4-apispy-24-09-2026.m4a
```

Si el nombre está bien, el resto funciona sin intervención. Si está mal, el notebook avisa pero el archivo termina en `_sin_materia`.

## Qué hay que decidir y qué se deriva

El formato tiene cinco campos, pero no hay que escribirlos todos:

| Campo | De dónde sale |
|---|---|
| `ucab` | constante |
| `w2` | la semana actual, se cambia una vez por semana |
| `d4` | se deriva del día de la semana de la fecha del archivo |
| `apispy` | **lo único que se elige por grabación** |
| `24-09-2026` | la fecha del archivo, que el teléfono ya guarda |

O sea que el trabajo real por clase es **elegir la materia de una lista**.

## Opción A: a mano

Grabar, y al final de la semana renombrar los archivos desde el explorador del teléfono antes de subirlos. La convención está pensada para escribirse a mano sin ambigüedad.

Es más trabajo por semana, pero no depende de instalar nada.

## Opción B: automatizado con Tasker

Android no trae un sistema de atajos equivalente al de iOS. Para este flujo sirve **Tasker**, que tiene juntas las tres piezas necesarias: diálogos de selección, operaciones de archivo y un intérprete de JavaScript.

El flujo completo, con el código del JavaScriptlet que deriva el día de la semana, está en el **Anexo A** del notebook ([`tools/transcriptioner.ipynb`](../tools/transcriptioner.ipynb)).

En resumen:

1. Variables globales: `%INSTITUCION`, `%SEMANA` (se actualiza cada lunes),
   `%ORIGEN`, `%DESTINO`, `%MATERIAS`.
2. `List Dialog` sobre `%MATERIAS` → elegir la materia.
3. `Test File` → fecha de modificación del archivo.
4. `JavaScriptlet` → calcula `%DIA` y `%FECHA_NOMBRE`.
5. `File Move` → renombra y mueve a `%DESTINO`.

**Que `%MATERIAS` coincida exactamente con los códigos de `subjects/`** es lo que evita que una variante cree una carpeta duplicada.

## La subida

**Autosync for Google Drive** (MetaCtrl) vigila la carpeta local y sube sola.

- **Local**: la carpeta destino de Tasker.
- **Remota**: `google_colab/transcriptioner/audios/week_N`.
- **Método**: *Upload only*. Con sincronización bidireccional, cualquier cosa que se borre de Drive se borraría también del teléfono.
- **Solo con WiFi**: una clase de dos horas pesa entre 60 y 120 MB.

La carpeta remota lleva el número de semana, así que hay que cambiarla cada lunes junto con `%SEMANA` en Tasker. Son dos ediciones semanales en el mismo momento.
