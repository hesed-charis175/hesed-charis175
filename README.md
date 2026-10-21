# Hi, I'm Hesed Charis Bayiha

**Programmer and independent researcher: programming languages, adaptive control, and algorithms.**

🌐 [hesed-charis.vercel.app](https://hesed-charis.vercel.app)

---

## Risk: a systems programming language

A statically typed, systems-level language with explicit memory management. The compiler, `riskc`, is a single-pass compiler written in C++17 that lowers Risk to C99 and hands it to GCC for a native executable.

```
main.risk → riskc → C99 → GCC → native executable
```

```
func main() -> i32 {
    println("Hello, Risk!");
    return 0;
}
```

- Static type checking before code generation
- Standard library written in Risk
- Reference counting and arena allocation planned
- Used to build a CNN for MNIST, a TUI file explorer and a PID pendulum simulator

[Source](https://github.com/hesed-charis175/Risk) · [Playground](https://risk-playground-web.vercel.app/) · [Releases](https://github.com/hesed-charis175/risk-releases) · [Dev logs](https://hesed-charis.vercel.app/projects/risk-programming-language)

---

## Adaptive control: Neuro-Plastic Network on a Wheeled Inverted Pendulum

A robot balances on one wheel while its leg length and mass change between four hidden configurations without warning. The controller sees two noisy tracking-error numbers per tick and outputs one wheel torque.

The solution is a bank of tiny recurrent neurons, each 15 numbers. Each neuron predicts the next observation and carries a controller for the regime it has learned. The neuron currently predicting best drives the robot, so it also acts as a regime detector. The bank adapts its own structure:

- **Spawn** a neuron when no existing one predicts well for long enough
- **Prune** neurons that are never used
- **Merge** neurons that learned the same thing
- **Learn only when winning**, so earlier regimes aren't overwritten

Control weights are trained without a plant model. Built as a C++ simulator with a Dear ImGui interface.

[Source](https://github.com/hesed-charis175/NPRN_Sim) · [Write-up](https://hesed-charis.vercel.app/projects/neuro-plastic-network-on-a-wheeled-inverted-pendulum)

---

## Research: maze exploration with local observation

An agent's configuration on a grid can be recovered from its action stream alone. These two papers, published on Zenodo, establish this for maze exploration under local observation, and I argue it extends to any grid. My longer-term goal is the generalization that applies to non-orthogonal tessellations as well.

### Deterministic String Rewriting: Post-Hoc Optimization for Local-Observation Maze Exploration
An explorer's actions form a stream of symbols. A single deterministic rewriting algorithm collapses redundant detours in that stream into a shorter path without re-observing the maze. The formalization uses rewriting systems, the algebra of the free monoid of actions, and homotopy contraction of loops. The natural greedy version is shown to be **not confluent** on multiply-connected mazes, and a **Jump-Graph** algorithm fixes it by choosing the provably optimal set of loop removals in one sweep.

**Result:** 100% success; average path reduction of **65%** (singly-connected) and **88%** (multiply-connected).
[DOI: 10.5281/zenodo.23018157](https://doi.org/10.5281/zenodo.23018157)

### Prospective Closure Detection on the Action Stream: Online Left-Wall-Following for Multiply-Connected Mazes
Left-wall-following is complete on simply-connected mazes but circles islands forever on multiply-connected ones. I derive an exact criterion on the action stream for detecting when a stretch of movement returns the agent to its starting cell, reduced to one set-membership test per step. Applied before each move commits, it becomes an online rule that, with a backtracking stack, **provably equals depth-first search** and is complete on any finite connected grid maze in O(|V|) memory. Compared analytically and empirically with Trémaux's and Pledge's algorithms.

**Result:** on 500 random multiply-connected mazes it matched reference DFS exactly and covered every maze; naive left-wall-following failed all 90 high-cyclicity trials.
[DOI: 10.5281/zenodo.23122471](https://doi.org/10.5281/zenodo.23122471)

---


✍️ More writing on my [blog](https://hesed-charis.vercel.app/blog).
