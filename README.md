[![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)

# RL Infinite Loop Demo

A small interactive demo showing how an RL agent gets stuck in an infinite loop when its policy has a bug — and how a simple cycle detection mechanism pulls it out.

## What it shows

RL agents follow a policy: given a state, do this action. When that policy has flaws, the agent can bounce between the same states forever without ever reaching the goal. It's a common failure mode, and it shows up not just in classic RL but also in **LLM-based agents**.

The setup is a **3×3 grid world**:

- Agent starts at `(0,0)`, goal at `(2,2)`, wall at `(1,1)`
- The policy has a deliberate bug: at `(1,2)` — one step above the goal — the agent moves **left** instead of down, colliding with the wall and looping forever

## [→ Live demo](https://jhonzacipa.github.io/rl-cycle-demo/)

## Two scenarios, side by side

- **No protection** — the buggy policy runs unchecked. The agent never reaches the goal.

- **Cycle detection** — same bad policy, but the agent tracks how many times it visits each state. Once a threshold is hit, it ignores the policy and picks a random action instead. That's enough to break the cycle.

## Other ways to handle this

| Technique | How it helps |
|-----------|-------------|
| **Max steps** | Cut the episode after N steps |
| **Step penalty** | Small negative reward per action discourages wandering |
| **Cycle detection** | What this demo uses — track visits, force exploration |
| **ε-Greedy** | Random action with probability ε regardless of policy |
| **Curiosity / intrinsic reward** | Reward the agent for visiting new states |
| **Discount factor γ < 1** | Long cycles become less attractive |

## Running it locally

No dependencies, just open the HTML file.

```bash
git clone https://github.com/JhonZacipa/rl-cycle-demo.git
cd rl-cycle-demo
open index.html
