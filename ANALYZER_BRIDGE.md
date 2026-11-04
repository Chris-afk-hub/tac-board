# Puente de posiciones reales HBR2 → Tac-Board

Este parche modifica el analizador de HaxBall para exportar posiciones **obtenidas del motor de simulación**, no posiciones inventadas.

## Qué hace

- Reinicia la línea de tiempo exportada al cargar una repetición.
- Lee la pelota desde `d[0].a` y los discos de jugadores desde `b[i].H.a` dentro del callback de simulación.
- Envía un fotograma individual cada 60 ticks (aprox. 1 segundo), evitando retransmitir toda la línea de tiempo en cada actualización.
- Cada fotograma incluye `timeSec`, la pelota y los jugadores, y se envía a la pestaña que abrió el analizador mediante `window.opener.postMessage`.
- Conserva nombres y equipos tal como los entrega el motor.

## Aplicación

1. Hacé un fork de https://github.com/haxball-replay-analyzer/haxball-replay-analyzer.github.io en tu cuenta.
2. En el fork, abrí `src/game2.js` y aplicá los dos cambios de `analyzer-bridge.patch` (el parche está escrito contra la rama `react`).
3. Renombrá el repositorio del fork a `haxball-replay-analyzer`. En `package.json`, cambiá `homepage` a `https://chris-afk-hub.github.io/haxball-replay-analyzer/`. Luego ejecutá `npm install` y `npm run deploy` desde el repositorio para generar la rama `gh-pages`; activá GitHub Pages desde esa rama y la carpeta raíz. La URL publicada debería ser `https://chris-afk-hub.github.io/haxball-replay-analyzer/`.
4. Abrí Tac-Board y, desde ahí, abrí tu analizador personalizado en otra pestaña. Es importante que la pestaña del analizador sea abierta desde Tac-Board para que exista `window.opener`.
5. En Tac-Board, pegá `https://chris-afk-hub.github.io/haxball-replay-analyzer/` en el campo de URL y pulsá **Abrir analizador personalizado**. Cargá el mismo archivo `.hbr2` en esa pestaña. Al reconstruirse el partido, el analizador enviará los fotogramas a Tac-Board. El botón **Analizar repetición** se habilita cuando llega el primer fotograma y resume cuántos se recibieron.

## Importante

El analizador público original no contiene este parche y, por lo tanto, no envía coordenadas a Tac-Board. Este archivo prepara el cambio de motor, pero **no significa que la sincronización ya esté publicada o probada**.

El puente usa como origen de destino `https://chris-afk-hub.github.io`, que corresponde a GitHub Pages del proyecto Tac-Board. Si publicás el fork bajo otro dominio, cambiá ese origen tanto en el parche como en el receptor de `index.html`.

La extracción actual exporta un fotograma por segundo. La línea de tiempo corresponde a los ticks procesados por el motor desde que se carga la repetición.
