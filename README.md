# Tac-Board — HaxBall Tactical Studio

Pizarra táctica web para preparar jugadas de HaxBall.

## Funciones
- Cancha editable con jugadores rojos/azules y pelota.
- Herramientas de mover, flechas, zonas y goma de borrar por clic sobre el objeto o el trazo.
- Secuencias de varios pasos con reproducción animada.
- Plantillas de córner, presión alta y defensa.
- Tamaño de cancha, zoom y radios configurables.
- Selector de canchas: Futx3, Futx5, Futx7 y Rsx4. Futx3 usa el archivo de estadio HBS «Futsal x3 by Bazinga» compartido para trazar sus líneas y áreas.
- Pantalla grande a pantalla completa, con el campo ampliado y un desplegable para bajar/ocultar herramientas y controles. Las coordenadas del cursor se ajustan al escalado del SVG.
- Modo solo vista para mostrar el tablero sin permitir ediciones.
- Importar/exportar jugadas en JSON.
- Lector inicial de archivos `.hbr2`: valida la cabecera HBR2, lee versión y duración, y permite seleccionar un minuto.

## Nota sobre los mapas
Las cuatro canchas incluidas son diseños visuales base adaptados a cada formato. No se presentan como copias exactas de mapas originales de Bazinga; para reproducirlos con precisión hacen falta sus archivos de estadio o capturas de referencia.

## Análisis de replays: estado actual
La pantalla REC todavía no reconstruye las posiciones de jugadores y pelota. Los archivos HBR2 almacenan entradas/eventos y requieren simular la repetición con el motor de HaxBall para recuperar las coordenadas. La aplicación no inventa posiciones ni presenta una vista aproximada como si fuera real. El botón de la pantalla REC abre el analizador comunitario como herramienta externa.

## Publicar con GitHub Pages
En el repositorio: **Settings → Pages → Deploy from a branch → main → /(root) → Save**. Luego la web queda en:
`https://chris-afk-hub.github.io/tac-board/`

## Uso
Abrí la página en un navegador moderno. No requiere instalación ni servidor propio. Los archivos seleccionados se leen localmente en el navegador.

## Formato de jugadas
Las jugadas se guardan como JSON con el identificador `haxball-tac-board`, versión 2.
