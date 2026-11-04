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
- Lector inicial de archivos `.hbr2`: valida la cabecera HBR2 y lee versión y duración.
- Acceso directo al [HaxBall Replay Analyzer](https://haxball-replay-analyzer.github.io/) (licencia MIT) en una pestaña nueva; se evita la incrustación que no carga de forma fiable.

## Nota sobre los mapas
Las cuatro canchas incluidas son diseños visuales base adaptados a cada formato. No se presentan como copias exactas de mapas originales de Bazinga; para reproducirlos con precisión hacen falta sus archivos de estadio o capturas de referencia.

## Análisis de replays: estado actual
La pantalla REC valida la cabecera HBR2, muestra la duración y permite elegir minuto y segundo con precisión de un segundo. El reproductor de [HaxBall Replay Analyzer](https://github.com/haxball-replay-analyzer/haxball-replay-analyzer.github.io), publicado bajo licencia MIT, se abre en una pestaña nueva porque la versión incrustada no carga de forma fiable. El archivo debe seleccionarse nuevamente allí: el navegador no permite transferir automáticamente el archivo local a otra web. La hora elegida en Tac-Board es una referencia y todavía no busca ese instante en el reproductor externo. La pizarra aún no dibuja las posiciones reales: falta integrar el motor de simulación HBR2 y exportar las coordenadas por tick de jugadores y pelota.

## Publicar con GitHub Pages
En el repositorio: **Settings → Pages → Deploy from a branch → main → /(root) → Save**. Luego la web queda en:
`https://chris-afk-hub.github.io/tac-board/`

## Uso
Abrí la página en un navegador moderno. No requiere instalación ni servidor propio. Los archivos seleccionados se leen localmente en el navegador.

## Formato de jugadas
Las jugadas se guardan como JSON con el identificador `haxball-tac-board`, versión 2.


### Integración de posiciones REC (en desarrollo)

La cancha REC ahora incluye una capa SVG y un receptor de mensajes para fotogramas reconstruidos. El formato esperado es un mensaje `postMessage` desde `https://haxball-replay-analyzer.github.io` con `type: "TACBOARD_HAXBALL_REPLAY_FRAMES"`, `stadium: { width, height }` y `frames` (un fotograma por segundo, con `ball: { x, y }` y `players: [{ name, team, x, y }]`). Al elegir un segundo, Tac-Board dibuja los jugadores y la pelota usando coordenadas del estadio.

**Pendiente para que funcione con archivos reales:** conectar el motor HBR2 para que envíe esos fotogramas. El analizador actual calcula posiciones de jugadores internamente, pero no publica ese protocolo ni envía las coordenadas de la pelota a Tac-Board. Por eso esta capa de dibujo no debe confundirse con una integración completa del motor.
