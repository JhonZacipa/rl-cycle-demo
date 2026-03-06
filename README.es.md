
***

## `README.es.md` (Español)

```markdown
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)

# RL Infinite Loop Demo

Un demo interactivo que muestra cómo un agente de RL puede quedar atrapado en un loop infinito cuando su política tiene un bug — y cómo un mecanismo simple de detección de ciclos logra sacarlo.

## Qué muestra

Los agentes de RL siguen una política: dado un estado, ejecuta esta acción. Cuando esa política tiene fallas, el agente puede rebotar entre los mismos estados para siempre sin llegar nunca a la meta. Es un fallo bastante común, y no aparece solo en RL clásico sino también en **agentes basados en LLMs**.

El escenario es un **grid world de 3×3**:

- El agente empieza en `(0,0)`, la meta está en `(2,2)`, hay una pared en `(1,1)`
- La política tiene un bug intencional: en `(1,2)` — un paso arriba de la meta — el agente se mueve **a la izquierda** en vez de bajar, choca con la pared y se queda en loop para siempre

## [→ Demo en vivo](https://jhonzacipa.github.io/rl-cycle-demo/)

## Dos escenarios en paralelo

- **Sin protección** — la política con bug corre sin control. El agente nunca llega a la meta.

- **Con cycle detection** — misma política, pero el agente rastrea cuántas veces visita cada estado. Al superar un umbral, ignora la política y elige una acción aleatoria. Eso es suficiente para romper el ciclo.

## Otras formas de manejar esto

| Técnica | Cómo ayuda |
|---------|-----------|
| **Max steps** | Cortar el episodio después de N pasos |
| **Step penalty** | Recompensa negativa por paso, desalienta el vagabundeo |
| **Cycle detection** | Lo que usa este demo — rastrear visitas y forzar exploración |
| **ε-Greedy** | Acción aleatoria con probabilidad ε sin importar la política |
| **Curiosity / intrinsic reward** | Recompensar al agente por visitar estados nuevos |
| **Discount factor γ < 1** | Los ciclos largos se vuelven menos atractivos |

## Correrlo localmente

Sin dependencias, solo abre el HTML.

```bash
git clone https://github.com/JhonZacipa/rl-cycle-demo.git
cd rl-cycle-demo
open index.html
