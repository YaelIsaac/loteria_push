# Lotería Push · Notificaciones push (FCM) en Flutter con TDD

**Materia:** Desarrollo de Aplicaciones Móviles
**Alumno:** González López Yael Isaac
**Fecha:** 23 de noviembre de 2026

## Descripción

Lotería mexicana donde el cantor vive en un servidor en Node. Cada carta que canta llega como notificación push (Firebase Cloud Messaging) al teléfono de todos los jugadores de la sala, y a quien le falta una sola carta para completar un patrón le llega un aviso personal de "¡Casi!". La app trata cada push como texto no confiable: valida su forma, aplica las cartas en orden, detecta huecos si se perdió una y se pone al día con el servidor. Si el usuario no da permiso de notificaciones, la app consulta al cantor cada 5 segundos mientras está abierta. El servidor baraja con Fisher-Yates, colapsa mensajes viejos, borra tokens muertos y nunca expone secretos. Todo se desarrolló con TDD: 61 pruebas en el servidor y 52 en la app.

## Estructura del proyecto

<!-- PEGA AQUÍ LA CAPTURA -->

## Pruebas de casos (éxito y fallo)

## Pruebas del servidor (61) · server/test/

Pruebas: baraja (54 cartas y mezcla Fisher-Yates), líneas y patrones de la tabla, armado de mensajes push con colapso, sala del juego con el aviso de "¡Casi!" y servidor HTTP de punta a punta (errores, límites y secretos).

### Éxito (todas en verde)

<!-- PEGA AQUÍ LA CAPTURA -->

### Fallo (hay 54 cartas con ids 1..54)

<!-- PEGA AQUÍ LA CAPTURA -->

## Pruebas de eventos y patrones (17) · test/evento_lineas_test.dart

Pruebas: leer un push con desconfianza (tipos, números en rango y textos raros) y los mismos patrones de la tabla que el servidor.

### Éxito (todas en verde)

<!-- PEGA AQUÍ LA CAPTURA -->

### Fallo (carta válida con números en texto)

<!-- PEGA AQUÍ LA CAPTURA -->

## Pruebas de la partida (10) · test/partida_test.dart

Pruebas: aplicar cartas en orden, ignorar repetidas, detectar huecos y aplicar lotes desordenados.

### Éxito (todas en verde)

<!-- PEGA AQUÍ LA CAPTURA -->

### Fallo (las cartas en orden se aplican)

<!-- PEGA AQUÍ LA CAPTURA -->

## Pruebas del controlador (22) · test/controlador_test.dart

Pruebas: unirse con y sin permiso, suscribirse al tema de la sala, actualizar el token, abrir desde una notificación, ponerse al día, errores de red y salir.

### Éxito (todas en verde)

<!-- PEGA AQUÍ LA CAPTURA -->

### Fallo (unirse con permiso: registra el destino y se suscribe al tema de la sala)

<!-- PEGA AQUÍ LA CAPTURA -->

## Pruebas de pantalla (3) · test/pantalla_test.dart

Pruebas: la sala en espera con el aviso de que no hay push, la carta cantada en la tabla y el aviso de "¡Casi!".

### Éxito (todas en verde)

<!-- PEGA AQUÍ LA CAPTURA -->

### Fallo (muestra la sala, la espera y el aviso de que no hay push)

<!-- PEGA AQUÍ LA CAPTURA -->

## Todas las pruebas de Flutter en verde (52)

<!-- PEGA AQUÍ LA CAPTURA -->

## Evidencia de la aplicación

### Cantor: sala creada y cartas cantadas

<!-- PEGA AQUÍ LA CAPTURA -->

### Jugador: tabla con la carta cantada

<!-- PEGA AQUÍ LA CAPTURA -->

### Servidor mostrando los push enviados

<!-- PEGA AQUÍ LA CAPTURA -->

## Conclusión

Con TDD el juego se armó desde el servidor hacia la app: primero las reglas (baraja, patrones y mensajes), luego la sala y el servidor HTTP, y al final la app que recibe los push. Las capturas de fallo demuestran que las pruebas sí detectan errores. Como Firebase quedó detrás de interfaces (el enviador en el servidor y el puerto push en la app), todo se probó sin cuenta de Firebase ni internet, y la app no se rompe cuando un mensaje llega tarde, repetido, desordenado o con datos raros.
