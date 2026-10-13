<!--
EJEMPLO ILUSTRATIVO. No es una clase real: está escrito a mano para mostrar
cómo sale una transcripción automática, con los errores típicos del reconocimiento de voz. Sirve para que se vea de qué parte la nota de ejemplo.
-->

---
source: ucab-w2-d4-apispy-24-09-2026.m4a
institucion: ucab
materia: apispy
semana: 2
dia_semana: 4
fecha: 2026-09-24
model: large-v3
language: es
duration: 00:14:32
transcribed_at: 2026-09-28T19:42:11
tool: oido v0.4 (colab)
---

Bueno muchachos vamos a arrancar, hoy vamos a ver fasta pi que es el framework que vamos a usar todo el semestre

La idea es que ustedes ya saben hacer una api con flask verdad, el año pasado lo vieron, entonces fasta pi hace lo mismo pero con dos cosas que flask no tiene

La primera es que valida solo, ustedes definen el tipo de dato y él se encarga de verificar que lo que llega cumpla, eso lo hace con pidantic que lo vamos a ver la clase que viene

La segunda es que genera la documentación sola, ustedes levantan el servidor y se van a barra docs y ya está toda la documentación ahí

Entonces lo mínimo es esto, importan fasta pi, crean la instancia, y decoran la función con app punto get

Un decorador si no se acuerdan es eso que va con arroba arriba de la función

Ojo con esto que siempre se equivocan, el orden de las rutas importa, si ustedes ponen barra items barra algo antes que barra items barra el id, entonces [inaudible] va a tomar la primera que coincida

Esto va para el examen, acuérdense, el orden importa

Para los parámetros tienen dos formas, los que van en la ruta que se llaman path parameters y los que van después del signo de interrogación que son los query parameters

Los primeros son obligatorios porque forman parte de la ruta, los segundos son opcionales y ustedes le pueden poner un valor por defecto

Ah y una cosa, para correr esto no usan python archivo punto py, usan [se corta el audio] con reload para que se reinicie solo cuando ustedes guarden

Bueno la semana que viene vemos pidantic en profundidad, lean la documentación de fasta pi la parte de first steps que está muy bien
