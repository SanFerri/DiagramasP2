# Archivo que explica el comportamiento de cada clase

## Game - Structurer
Es la clase que contiene información sobre una partida, contiene los datos necesrios para que ésta se lleve a cabo. 
Se almacenan dos instancias de Board por cada Player, de los cuales hay dos en total por partida. Almacena también el estado de la partida y el jugador que se supone debe realizar el siguiente movimiento.

## GameStatus - Enumerador
Enumerador que contiene todos los estados posibles de un juego, no contiene lógica.

## Container - Information holder
Guarda instancias de un tipo genérico pasado por párametro. Se trata de un manager por lo que es un Singletton.

## GameContainer - Information holder
Container para las instancias de objetos tipo Game (juegos).

## UserContainer - Information holder
Container para las instancias de tipo User (jugadores).

## User - 

## Board

