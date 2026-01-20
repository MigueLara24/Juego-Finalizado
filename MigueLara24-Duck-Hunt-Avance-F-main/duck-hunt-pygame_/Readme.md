# Duck Hunt – Prototipo Retro en Pygame

## Descripción
Este proyecto prototipo funcional inspirado en el videojuego clásico
Duck Hunt. El objetivo principal es recrear la mecánica básica del juego, enfocándose en
el movimiento del pato y la acción de disparo, manteniendo un estilo retro.

-El proyecto representa un avance inicial y no una versión final del videojuego.

## ENFOQUE DEL JUEGO
- Duck Hunt Ultimate Edition es un juego de puntería mejorado con:
Modo Historia: 4 capítulos con narrativa progresiva (día, atardecer, noche)
Modo Arcade: Juego infinito con dificultad creciente
Modo Secreto: 5 jefes con habilidades especiales (desbloqueable)
Sistema de Combos: Movimientos secretos para activar power-ups
QTE (Quick Time Events): Minijuegos de reacción en modo secreto
Historia emocional: Un perro cazador alimentando a sus cachorros

## Controles
El juego está diseñado para ser utilizado con un mando clásico de Nintendo, reforzando la
experiencia retro del videojuego.

- En Menú:
W / S: Navegar opciones
ESPACIO: Seleccionar
ESC: Salir al menú / Salir del juego

- En Juego:
WASD: Mover la mira
ESPACIO: Disparar
R: Recargar (3 balas)
ESC: Pausar / Volver al menú

## Explicación del Código - LIBRERÍAS PRINCIPALES
import pygame
import random
import math
import time
from collections import deque
-pygame: Biblioteca principal para gráficos, sonido y eventos
-random: Para generar posiciones y comportamientos aleatorios
-math: Para cálculos trigonométricos y físicos
-deque: Para manejo eficiente de diálogos en cola

## SISTEMA DE SONIDO (Líneas 93-210)
class SoundSystem:
    def __init__(self):
        self.sounds = {}
        self.current_ambient = None
        self.volume = 0.4
        self.generate_all_sounds()

Clase que genera sonidos proceduralmente
Usa ondas sinusoidales para crear efectos de sonido
Controla música ambiental y efectos

## Sistema de Combos (Líneas 2480-2520)
 Detección de combos
combo_keys.append(key_map[event.key])
combo_str = ''.join(combo_keys)
if combo_str.endswith('AWSD'):
    dog.activate_god_mode()

## Bucle Principal (Líneas 2570-3400)
while running:
    # 1. Manejo de eventos
    # 2. Actualización de estado según game_state
    # 3. Renderizado según game_state
    # 4. Control de FPS (con slow motion)

## CONTROL DE DISPAROS Y COLISIONES (Líneas 2602-2667)
if event.key == pygame.K_SPACE and ammo > 0:
    for duck in ducks:
        result = duck.check_hit(cursor_x, cursor_y)
        if result == True:
            score += duck.points
            ducks_hit += 1

Sistema de detección de colisiones

Puntos basados en tipo de pato y multiplicadores

## Comandos

Comando	-> Efecto -> Duración
AWSD = Modo Dios (el perro mata patos automáticamente)	-> 5s, 1 vez por ronda
DSA	= Munición infinita -> 5s
WDS	= Cámara lenta -> 5s
ADAD = Puntos dobles -> 10s
- WSADWSAD = DESBLOQUEA MODO SECRETO -> Permanente

## MODOS DE JUEGO
4.1 Modo Historia (4 Capítulos)
Capítulo 1 - El Amanecer: Día, patos lentos, tutorial
Capítulo 2 - La Tarde Dorada: Atardecer, patos más rápidos
Capítulo 3 - Cacería Nocturna: Noche, visibilidad reducida
Capítulo 4 - El Desafío Final: Noche con más patos

4.2 Modo Arcade
Dificultad incremental infinita
Sin narrativa
Puntaje alto permanente

4.3 Modo Secreto (5 Jefes)
Requisito: Completar WSADWSAD en cualquier momento
Jefes:
SOMBRA ALADA (1000 pts) - Teletransporte, clones
FÉNIX OSCURO (1500 pts) - Renacimiento, estela de fuego
ESPECTRO DEL VACÍO (2000 pts) - Invencibilidad temporal, ráfagas
DEMONIO CARMESÍ (2500 pts) - Charco de sangre, furia
TITÁN INFERNAL (5000 pts) - Terremotos, meteoros, apocalipsis

## Puntajes mínimos por ronda
Ronda 1: 300 pts
Ronda 2: 600 pts
Ronda 3: 1000 pts
Ronda 4: 1500 pts
Ronda 5: 2200 pts

## SISTEMA DE POWER-UPS
Aparecen aleatoriamente durante el juego:

Icono	Tipo	Efecto	Duración
⚡	Rayo	Disparo rápido (menos delay)	5s
⏱️	Reloj	Cámara lenta	5s
🎯	Balas	+5 munición	Instantáneo
★	x2 Puntos	Puntos dobles	10s
🛡️	Escudo	Protección (visual)	5s
🧲	Imán	Atrae power-ups desde lejos	5s

## SISTEMA QTE (Quick Time Events)
Solo en Modo Secreto:
Aparecen aleatoriamente
Presionar teclas en secuencia (W,A,S,D,Q,E,R,F)
Éxito: +150 a +525 puntos (según dificultad)
Fallo: -150 a -525 puntos

Tiempo límite: 1.0s a 3.3s

## Estados del Juego (game_state)
'intro': Menú principal
'controls': Pantalla de controles
'story_intro': Introducción narrativa
'secret_intro': Introducción modo secreto
'boss_presentation': Presentación de jefes
'chapter_intro': Introducción de capítulo
'playing': Juego activo
'round_end': Fin de ronda
'game_over': Derrota

## Estados del Perro (Dog.state)
'hidden': Escondido en la hierba
'laughing': Ríe cuando fallas
`'celebrating'**: Celebra un pato cazado
'god_mode': Modo dios activo
'hiding': Volviendo a esconderse
'victory': Victoria


## REQUISITOS Y DEPENDENCIAS
# Requerido:
import pygame
import random
import math
import time
from collections import deque

# Versión: Python 3.8+
# Pygame: 2.0+
# No requiere assets externos (todo procedural)

## LÓGICA DE DIFICULTAD
Capítulo 1: speed = 2.0
Capítulo 2: speed = 2.6
Capítulo 3: speed = 3.2
Capítulo 4: speed = 3.8
Secreto
Jefe 1: speed = 3.0, vida = 3
Jefe 2: speed = 3.5, vida = 4
Jefe 3: speed = 4.0, vida = 5
Jefe 4: speed = 4.5, vida = 6
Jefe 5: speed = 5.0, vida = 8

Arcade
speed = 2.0 + (round_num * 0.6)

## CONSEJOS DE JUEGO
Priorizar combos: AWSD (Modo Dios) es extremadamente útil
Administrar munición: Recargar antes de quedarse sin balas
Modo Secreto: Practicar QTE para bonificaciones grandes
Power-ups: El imán es útil para recolectar otros power-ups
Jefes: Apuntar cuando no están en estado invencible (parpadeo)

## CRÉDITOS TÉCNICOS
Motor: Pygame 2.0+
Gráficos: Renderizado procedural
Sonido: Generación procedural de ondas
Desarollado por: Miguel Lara
Versión: 3.0 Ultimate Edition

## Estado del Proyecto
Este proyecto corresponde a un avance funcional enfocado en:
- Movimiento del personaje
- Acción básica
- Entorno simple
- Control retro mediante mando
- Variedad de Modos de Juegos
- Implementaciones creativas del estudiante
- Similitud con el enfoque del juego original

## Arquitectura del Código
duck_hunt_ultimate.py
├── CONSTANTES (colores, dimensiones)
├── SoundSystem (sonidos generados proceduralmente)
├── AmbientSound (gestor de audio)
├── Cloud (nubes animadas)
├── Star (estrellas para noche)
├── Dog (perro cazador con estados)
├── ScreenShaker (efectos de pantalla)
├── DialogueSystem (sistema de diálogos)
├── Particle (sistema de partículas)
├── FloatingText (textos flotantes)
├── PowerUp (power-ups coleccionables)
├── QTESystem (minijuegos QTE)
├── Duck (patos y jefes)
├── Funciones de dibujo (background, HUD, etc.)
└── main() (bucle principal del juego)