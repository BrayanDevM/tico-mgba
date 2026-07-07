# Notas de release — 1.1.2 (borrador)

> Versión propuesta, no publicada todavía. Recuerda antes de crear el release: bumpear `"1.1.1"` → `"1.1.2"` en `build_mgba_nro.sh` (línea del `$NACPTOOL --create`), recompilar, y solo entonces taguear/publicar — igual que se hizo para 1.1.0/1.1.1. Cubre todo lo agregado desde el tag `1.1.1` (sin commits todavía, todo en el working tree).

## Añadido

- **Pantalla de Detalle del truco.** Con un truco seleccionado en Herramientas > Trucos, el botón **X** abre "Detalle de [nombre]": un selector de **Tipo de código** (Auto / GameShark / PAR, con ◄►) y, debajo, una vista previa de solo lectura del código crudo de ese truco.
- **Scroll en la vista previa.** Los trucos con muchas líneas de código (p. ej. "Todos los objetos en PC") se recorren con arriba/abajo, con los mismos indicadores ▲▼ que ya usa la lista de Trucos.
- **El tipo de código ahora se puede fijar desde el juego** y queda guardado en el `.cheats` de esa partida (como directiva `!GSAv1`/`!PARv3`, o sin directiva para Auto) — es la única propiedad de un truco que se persiste; el ON/OFF sigue sin guardarse entre sesiones, a propósito.

## Notas técnicas

- **Encabezados de otros formatos de cheats.** Si el `.cheats` de un juego tiene líneas que tico no interpreta — por ejemplo `cheats = N` (formato RetroArch) o `[Sección]` (formato EZ-Flash) — tico las ignora al aplicar los trucos, pero las conserva tal cual dentro del archivo si en algún momento necesita reescribirlo (por ejemplo, al cambiar el tipo de código de algún truco desde la pantalla de Detalle). No se interpretan, pero tampoco se borran.
- **Escritura del `.cheats`.** Cuando se guarda un cambio de tipo de código, tico reescribe el archivo completo de forma atómica (a un archivo temporal y luego se reemplaza) en vez de sobreescribir directamente, para minimizar el riesgo de dañar la base de trucos de ese juego si algo interrumpe el guardado a mitad de camino.
