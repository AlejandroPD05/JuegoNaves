# Asteroids

Clásico de Asteroids en canvas, sin dependencias ni build: **un `index.html` y
seis archivos de sonido**. Se abre con doble clic y se despliega en GitHub
Pages tal cual.

**▶ Jugar en vivo:** https://alejandropd05.github.io/JuegoNaves/

## Controles

| Tecla | Acción |
|---|---|
| `←` / `→` | Girar la nave |
| `↑` | Impulso |
| `Espacio` | Disparar |

En pantallas táctiles aparecen botones táctiles con `aria-label` solo cuando el
dispositivo los necesita (`pointer: coarse`).

## Qué incluye

- Niveles con dificultad creciente (+1 asteroide por nivel, +10 % de velocidad)
- 3 vidas con invulnerabilidad parpadeante al reaparecer
- Pantallas de estado: menú con controles visibles, pausa (`ESC` / `P`) y fin con reintento
- Game loop con `requestAnimationFrame` y delta-time (física independiente de la tasa de refresco)
- Récord persistido en `localStorage`
- Música que **acelera según el porcentaje de asteroides** que quedan
- Efecto CRT (scanlines, viñeta, flicker) con `prefers-reduced-motion`
- Slider de volumen persistido, con pool de hasta 5 sonidos simultáneos
- Spawn seguro: los asteroides nunca aparecen encima de la nave

## Arquitectura

Todo vive en `index.html`: CSS en `<head>` y JS al final (constantes → audio →
entrada → máquina de estados → ciclo rAF → render/colisiones).

La decisión es deliberada: cero dependencias significa cero roturas, apertura
instantánea y despliegue trivial. Dentro del fichero hay ~25 constantes
nombradas al principio (`AST_TAM`, `VEL_GIRO_NAVE`, `FPS`…), de modo que las
"reglas del juego" se leen de un vistazo.

```
index.html        HTML + CSS + JS del juego
sounds/           laser, thrust, hit, explode, music-low, music-high (.m4a)
```

## Desarrollo

No hay paso de build. Para iterar, abre las herramientas del navegador y
recarga; para probar el sonido con política de autoplay, sirve la carpeta:

```bash
npx serve .
```

## Roadmap conocido

- ✓ Game loop con `requestAnimationFrame` + delta-time (antes `setInterval` a 30 FPS)
- ✓ Pantallas de estado reales (inicio / pausa / fin con reintento) y controles visibles en el menú
- Escalado HiDPI (`devicePixelRatio`) para pantallas Retina
- Mute por teclado
