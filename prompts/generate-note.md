# Prompt - Generar una nota de clase

> Copiá todo lo que está debajo de la línea y pegalo como primer mensaje de un chat nuevo. Adjuntá además: el template de la nota, la ficha de la materia y la transcripción.

---

Vas a convertir la transcripción automática de una clase universitaria en una nota de estudio para Obsidian.

## Lo que te estoy pasando

1. **El template de la nota** (`note.md`): la estructura exacta que tiene que tener el resultado.
2. **La ficha de la materia** (`subjects/<codigo>.md`): de qué trata, qué stack usa, y una tabla de términos que la transcripción suele arruinar.
3. **La transcripción**: el archivo `.md` que salió del transcriptor.

## Qué es la transcripción y qué no

Es la salida de un reconocimiento automático de voz sobre el audio de una clase grabada desde un teléfono. Eso implica:

- **Los términos técnicos pueden estar mal.** "FastAPI" puede aparecer como "fasta pi". La tabla de la ficha de materia es tu primera referencia; si un término no está ahí pero el contexto lo hace evidente, corregilo.
- **La puntuación es aproximada** y las frases pueden estar cortadas donde el profesor hizo una pausa, no donde termina la idea.
- **Hay ruido**: cosas que dijo un compañero, interrupciones, el profesor hablando de algo administrativo, audio que no se entendió.
- **El encabezado del archivo** (el frontmatter) trae materia, semana, día y fecha. Esos datos son confiables y van tal cual a la nota.

## Tu tarea

Escribir la nota siguiendo el template, con el contenido de esa clase, explicado de forma que se entienda sin haber estado ahí.

No es un resumen ni una limpieza de la transcripción. Es una nota de estudio: ordenada por tema, con las explicaciones completadas hasta que cierren, y con los ejemplos del profesor desarrollados.

## Reglas

**1. Distinguí siempre lo que dijo el profesor de lo que agregás vos.**

Esta es la regla más importante, y la razón es práctica: en un examen se evalúa lo que se dio en clase, no lo que es cierto en general. Si la nota mezcla ambas cosas, deja de servir para estudiar.

- Lo que el profesor explicó va en el cuerpo de la nota.
- Lo que agregás para que se entienda va en un callout `> [!tip] Agregado para claridad`.
- Las formulaciones textuales que importan — una definición que va a caer, un criterio de evaluación, una advertencia — van en `> [!quote] Lo que dijo el profesor`.

**2. No completes lo que no entendiste.**

Si un tramo del audio quedó ininteligible, si un término no se puede deducir, o si el profesor dejó una idea a medias, **decilo** en un callout `> [!warning] Dudoso en la transcripción`. Nunca rellenes con lo que probablemente dijo.

Una nota que admite un hueco es útil. Una nota que inventa para tapar el hueco es peligrosa, porque no hay forma de saber qué parte es confiable.

**3. Enlaces de Obsidian: solo conceptos.**

- **Sí**: los conceptos clave como `[[FastAPI]]`, `[[normalización]]`, `[[inyección SQL]]`. Que todavía no exista esa nota no es un problema. En Obsidian un enlace sin resolver es una señal de qué falta escribir, y es así como se construye el grafo.
- **No**: enlaces a otras notas de clase. No sabés qué notas existen ni cómo se llaman, y un enlace inventado a `[[ucab-w1-d4-apispy-17-09-2026]]` ensucia el vault. Si el profesor se refirió a una clase anterior, mencionalo en prosa.

**4. Respetá el template, pero no lo rellenes a la fuerza.**

Si el profesor no marcó nada para el examen, omití la sección "Para el examen". Una sección vacía con texto de relleno es peor que no tenerla.

**5. Omití el ruido.** Lo administrativo (fechas de entrega aparte, cambios de aula, quién faltó) no va, salvo que sea sobre evaluaciones.

**6. El frontmatter sale de la transcripción.** `materia`, `semana`, `dia_semana` y `fecha` se copian del encabezado del archivo de origen. `fuente` es el nombre del archivo de transcripción. Los `tags` los decides a partir del contenido.

## El resultado

Un solo archivo markdown, completo, listo para pegar en el vault.

El nombre del archivo es **el mismo que el de la transcripción**. Si la transcripción es `ucab-w2-d4-apispy-24-09-2026.md`, la nota se llama igual.

Antes de la nota, decime en dos o tres líneas qué tan buena estaba la transcripción: si hubo tramos perdidos, términos que tuviste que deducir, o partes donde no estás seguro. Eso me dice si vale la pena volver al audio.
