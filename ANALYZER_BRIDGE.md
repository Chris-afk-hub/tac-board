# Puente de posiciones reales HBR2 → Tac-Board

Este parche modifica el analizador de HaxBall para exportar posiciones **obtenidas del motor de simulación**, no posiciones inventadas. El cambio se aplica sobre la rama `react` del analizador.

## Qué hace

- Reinicia la línea de tiempo exportada al cargar una repetición.
- Lee la pelota desde `d[0].a` y los discos de jugadores desde `b[i].H.a` dentro del callback de simulación.
- Envía un fotograma individual cada 60 ticks (aprox. 1 segundo), evitando retransmitir toda la línea de tiempo en cada actualización.
- Cada fotograma incluye `timeSec`, la pelota y los jugadores, y se envía a la pestaña que abrió el analizador mediante `window.opener.postMessage`.
- Conserva nombres y equipos tal como los entrega el motor.

## Aplicación

1. Abrí https://github.com/haxball-replay-analyzer/haxball-replay-analyzer.github.io/fork y creá el fork en tu cuenta de GitHub.
2. Cuando termine, compartime el enlace del fork. Desde ahí puedo aplicar este parche sobre la rama `react` y preparar la publicación. No hace falta que edites el código a mano.
3. La publicación usará el nombre de repositorio `haxball-replay-analyzer` y la dirección `https://chris-afk-hub.github.io/haxball-replay-analyzer/`.
4. Después, en Tac-Board, pegá esa URL en el campo del analizador y pulsá **Configurar analizador con puente**. Cargá allí el mismo archivo `.hbr2`.
5. Al llegar los primeros fotogramas reales, se habilitará **Analizar repetición** en Tac-Board.

## Importante

El analizador público original no contiene este parche y, por lo tanto, no envía coordenadas a Tac-Board. Este archivo prepara el cambio de motor, pero **no significa que la sincronización ya esté publicada o probada**.

El puente usa como origen de destino `https://chris-afk-hub.github.io`, que corresponde a GitHub Pages del proyecto Tac-Board. Si publicás el fork bajo otro dominio, cambiá ese origen tanto en el parche como en el receptor de `index.html`.

La extracción actual exporta un fotograma por segundo. La línea de tiempo corresponde a los ticks procesados por el motor desde que se carga la repetición.
