# Transcripción: de Drive a `text/<materia>/`

El notebook [`tools/transcriptioner.ipynb`](../tools/transcriptioner.ipynb) corre `faster-whisper` sobre la GPU que Colab asigna gratis.

## Qué hace

Entra por semana, sale por materia:

```
audios/week_2/ucab-w2-d4-apispy-24-09-2026.m4a
        ↓
text/apispy/ucab-w2-d4-apispy-24-09-2026.md
```

El archivo de salida lleva un frontmatter con la materia, la semana, el día, la fecha y los datos de la corrida. Ese frontmatter es lo que la etapa siguiente usa para armar el encabezado de la nota.

## Cómo se corre

1. Abrir el notebook en Colab.
2. **Asignar GPU**: `Entorno de ejecución → Cambiar tipo de entorno → GPU`.
3. Ejecutar las secciones 1 y 2 — verifican el entorno e instalan el motor.
4. En la sección 3, ajustar `SEMANAS`:
   - `[]` → todas las semanas con audios pendientes
   - `[1, 3]` → solo esas
5. Ejecutar de la 3 a la 6.

La sección 4 muestra qué va a procesar y avisa de los nombres mal escritos antes de gastar GPU. Vale leerla antes de seguir.

## Lo que no hay que olvidar

**Lo ya transcrito se omite.** El criterio es la existencia del `.md` de salida, así que volver a correr después de una caída retoma donde quedó.

**Cada transcripción se escribe apenas termina**, y hay un guardado parcial cada cinco minutos de audio. Una caída a mitad de una clase de dos horas no pierde las dos horas.

**La pestaña tiene que quedar abierta** y la computadora sin suspender. Si se suspende, el navegador se desconecta y Colab termina la sesión.

## El límite de GPU

El tier gratuito de Colab no tiene un saldo visible: es una asignación dinámica que depende de cuánto se usó recientemente y de la demanda. Google no publica los límites ni cuánto duran las restricciones.

Medición propia: una semana de clases son ~16 horas de audio, que sobre una T4 son entre 1 y 2 horas de GPU.

Para estirar el uso:

- **Apagar el acelerador cuando no se está transcribiendo**
  (`Acelerador: Ninguno`). Una sesión con GPU asignada consume aunque no corra nada.
- **Cerrar la pestaña al terminar.**
- **Ir por tandas** en vez de todas las semanas juntas.
- **`MODELO = 'large-v3-turbo'`** en la sección 5: mismo encoder, decoder más liviano, bastante más rápido a cambio de algo de precisión.

Si se agota, lo ya transcrito está en Drive y no se pierde. Se retoma cuando vuelva.

## Errores conocidos

| Síntoma | Causa | Qué hacer |
|---|---|---|
| `FileNotFoundError: 'nvidia-smi'` | la sesión no tiene GPU | asignar GPU, o esperar a que vuelva la cuota |
| `CUDA driver version is insufficient` | lo mismo, visto desde la sección 2 | ídem |
| `Unable to load libcudnn...` | enlazador inconsistente | reiniciar sesión y correr desde la sección 2 |
| `CUDA out of memory` | modelo grande para la GPU | `MODELO = 'medium'` |
| `Operation not supported: /content/drive/...` | falta `MyDrive` en la ruta | ver `RAIZ` en la sección 3 |
| Menos de 2x realtime | está corriendo sobre CPU | verificar la sección 1 |
