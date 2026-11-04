# Tac-Board — HaxBall Tactical Studio

Pizarra táctica web para preparar jugadas de HaxBall.

## Funciones
- Cancha editable con jugadores rojos/azules y pelota.
- Herramientas de mover, flechas, zonas y goma de borrar.
- Secuencias de varios pasos con reproducción animada.
- Plantillas de córner, presión alta y defensa.
- Tamaño de cancha, zoom y radios configurables.
- Importar/exportar jugadas en JSON.
- Lector inicial de archivos `.hbr2`: valida la cabecera HBR2, lee versión y duración, y permite seleccionar un minuto.

## Análisis de replays: estado actual
La pantalla REC todavía no reconstruye las posiciones de jugadores y pelota. Los archivos HBR2 almacenan entradas/eventos y requieren simular la repetición con el motor de HaxBall para recuperar las coordenadas. La aplicación no inventa posiciones ni presenta una vista aproximada como si fuera real. El botón de la pantalla REC abre el analizador comunitario como herramienta externa.

## Publicar con GitHub Pages
En el repositorio: **Settings → Pages → Deploy from a branch → main → /(root) → Save**. Luego la web queda en:
`https://chris-afk-hub.github.io/tac-board/`

## Uso
Abrí la página en un navegador moderno. No requiere instalación ni servidor propio. Los archivos seleccionados se leen localmente en el navegador.

## Formato de jugadas
Las jugadas se guardan como JSON con el identificador `haxball-tac-board`, versión 2.

