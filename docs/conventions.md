# Convenciones

Este archivo es el contrato. Todo lo demás lo referencia en vez de repetirlo.

## Nombre de archivo de una clase

```
ucab-w2-d4-apispy-24-09-2026.m4a
│    │  │  │      └─ fecha de la clase, DD-MM-YYYY
│    │  │  └──────── código de la materia
│    │  └─────────── día de la semana, 1 = lunes … 7 = domingo
│    └────────────── semana del semestre
└─────────────────── institución
```

**El guion es el separador de campos**, así que ningún campo puede llevar guiones. La materia va toda junta: `ciberofflab`, no `ciberoff-lab`.

El mismo nombre, cambiando la extensión, viaja por toda la cadena:

| Etapa | Archivo |
|---|---|
| Audio | `ucab-w2-d4-apispy-24-09-2026.m4a` |
| Transcripción | `ucab-w2-d4-apispy-24-09-2026.md` |
| Nota de clase | `ucab-w2-d4-apispy-24-09-2026.md` |

El documento de estudio **no** sigue esta convención, porque no corresponde a una clase sino a un tema: `u02-fastapi.md`.

## La fecha es referencia, no clasificador

`w#` y `d#` son los que deciden a qué carpeta va cada cosa. La fecha está para que un humano sepa de cuándo es la clase sin abrir el archivo.

Consecuencia: **no hace falta declarar cuándo empezó el semestre** en ningún lado. La semana viene escrita.

Sí se verifica la coherencia entre ambos: el día de la semana de una fecha es intrínseco a esa fecha, así que si el nombre dice `d4` y el 24-09-2026 cae jueves, está bien; si dijera `d7`, hay un error de tipeo.

## Los dos nombres de cada materia

Cada materia tiene **dos** identificadores, y no son intercambiables:

| | Dónde se usa |
|---|---|
| **código corto** (`apispy`) | nombres de archivo, `text/`, `notes-vault/` |
| **nombre largo** (`apis-python`) | carpeta en `documents-vault/` |

**La correspondencia entre ambos vive en `subjects/<codigo>.md`**, en el frontmatter (`carpeta_notas` y `carpeta_documentos`). No hay una tabla centralizada a propósito: una sola fuente por materia no puede divergir consigo misma, dos listas sí.

## Estructura de carpetas

**En Drive**: entrada por semana, salida por materia:

```
google_colab/transcriptioner/
├── audios/week_N/      ← las grabaciones
└── text/<codigo>/      ← las transcripciones
```

**En `notes-vault`**: por código corto:

```
notes-vault/
└── <codigo>/           ← apispy/, bd/, ciberoff/ ...
    └── ucab-wN-dN-<codigo>-DD-MM-YYYY.md
```

**En `documents-vault`**: por nombre largo, con unidades:

```
documents-vault/
└── <nombre-largo>/     ← apis-python/, database-systems/ ...
    ├── register.md     ← el estado de la generación
    ├── u00-slug.md
    └── u01-slug.md
```

## Unidades de los documentos de estudio

`uNN-slug`, con `NN` de dos dígitos empezando en `00` y el slug en minúsculas con guiones.

**Los números son estables.** Una vez asignado, `u02` es ese tema para siempre. Si aparece material que conceptualmente va antes, se crea una unidad nueva con el número siguiente. Renumerar rompe nombres de archivo y enlaces del vault.

## Frontmatter

Cada tipo de archivo tiene su frontmatter, definido en su template:

| Archivo | Template |
|---|---|
| Nota de clase | [`templates/note.md`](../templates/note.md) |
| Documento de estudio | [`templates/study-document.md`](../templates/study-document.md) |
| Registro | [`templates/register.md`](../templates/register.md) |

El de la transcripción lo escribe el notebook, y lleva: `source`,
`institucion`, `materia`, `semana`, `dia_semana`, `fecha`, `model`,
`language`, `duration`, `transcribed_at`, `tool`.

## Obsidian: qué se usa y qué no

**Se usa**: frontmatter (propiedades), tags, callouts (`> [!note]`,`> [!tip]`, `> [!warning]`, `> [!quote]`, `> [!example]`, `> [!question]-`) y wikilinks.

**No se usa**: nada que dependa de un plugin. Dataview, Templater y similares quedan afuera para que los vaults se abran en cualquier instalación de Obsidian sin configurar nada.

**Wikilinks, con cuidado**: se enlazan conceptos (`[[FastAPI]]`), aunque la nota destino no exista todavía, un enlace sin resolver es una señal de qué falta escribir. No se enlaza entre vaults: no resuelve.
