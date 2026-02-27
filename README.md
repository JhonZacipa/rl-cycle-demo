# 🔁 RL Infinite Loop Demo

An interactive visualization that demonstrates how a Reinforcement Learning agent can get trapped in an infinite loop due to a poorly designed policy — and how cycle detection can rescue it.

## 🎯 What This Demonstrates

In Reinforcement Learning, an agent follows a **policy** that maps states to actions. If the policy has flaws, the agent can repeat the same actions indefinitely without ever reaching its goal. This is a well-known failure mode with real implications for RL systems, including LLM-based agents.

This demo presents a **3×3 grid world** where:

- 🤖 The agent starts at position `(0,0)`
- 🏆 The goal is at position `(2,2)`
- 🧱 A wall blocks position `(1,1)`

The agent's policy contains a bug: at position `(1,2)` — just one step above the goal — it moves left instead of down, causing it to bounce against the wall forever.

## 🖥️ Live Demo

**[👉 Open the Demo](https://jhonzacipa.github.io/rl-cycle-demo/)**

## 🔬 Side-by-Side Comparison

The demo runs two scenarios simultaneously:

| Scenario | Description | Outcome |
|----------|-------------|---------|
| 🔴 **No Protection** | Deterministic bad policy with no safeguards | Agent gets stuck in an infinite loop |
| 🟢 **Cycle Detection** | Same bad policy + visit counting + forced exploration | Agent escapes the cycle and reaches the goal |

### How Cycle Detection Works

1. The agent maintains a **history of visited states**
2. When a state has been visited more than a **threshold** number of times, a cycle is detected
3. Instead of following the flawed policy, the agent takes a **random alternative action**
4. This exploration breaks the cycle and allows the agent to discover a path to the goal

## 🛡️ Common Solutions for Infinite Loops in RL

| Technique | Description |
|-----------|-------------|
| **Max Steps** | Terminate episodes after N steps — the simplest safeguard |
| **Step Penalty** | Small negative reward per action, incentivizing shorter paths |
| **Cycle Detection** | Track state visits and force exploration on repetition |
| **ε-Greedy** | With probability ε, take a random action instead of the policy's choice |
| **Curiosity-Driven Exploration** | Intrinsic reward for visiting novel states |
| **Discount Factor (γ < 1)** | Future rewards decay, discouraging long cycles |

## 🚀 Usage

No dependencies required. Just open `index.html` in any modern browser.

```bash
git clone https://github.com/JhonZacipa/rl-cycle-demo.git
cd rl-cycle-demo
open index.html
```

### Controls

- **▶ Run** — Execute the simulation automatically
- **→ Step** — Advance one step at a time
- **↺ Reset** — Restart the simulation
- **Speed Slider** — Adjust animation speed (50ms–800ms)

## 📚 Context

This demo was built as part of my studies in **Artificial Intelligence (M.Sc.)** at Universidad de los Andes, exploring the intersection between Reinforcement Learning and LLM-based agents.

The same infinite loop problem applies to **LLM agents** that use tools: an agent might repeatedly reformulate a search query, retry a failed API call, or loop through the same reasoning steps. Frameworks like LangChain and AutoGen implement iteration limits for exactly this reason.

## 📄 License

MIT
