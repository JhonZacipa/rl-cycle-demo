# RL Infinite Loop Demo

A small interactive demo showing how an RL agent gets stuck in an infinite loop when its policy has a bug — and how a simple cycle detection mechanism pulls it out.

## What it shows

RL agents follow a policy: given a state, do this action. When that policy has flaws, the agent can bounce between the same states forever without ever reaching the goal. It's a common failure mode, and it shows up not just in classic RL but also in **LLM-based agents**.

The setup is a **3×3 grid world**:

- Agent starts at `(0,0)`, goal at `(2,2)`, wall at `(1,1)`
- The policy has a deliberate bug: at `(1,2)` — one step above the goal — the agent moves **left** instead of down, colliding with the wall and looping forever

## [→ Live demo](https://jhonzacipa.github.io/rl-cycle-demo/)

## Two scenarios, side by side

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
