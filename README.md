# desktop-familiar

A Windows-native embodied AI desktop companion: part assistant, part ambient interface, part executable agent.

`desktop-familiar` is not intended to be just a cute desktop pet.
It is designed as a **persistent personal agent shell** that can:
- listen through the microphone
- understand short-term user context
- remember long-term habits and preferences
- operate the desktop safely
- present itself as an always-available abstract companion

## Core idea
Most AI interfaces are trapped inside chat boxes.
This project explores a different thesis:

> an AI assistant becomes more useful when it is ambient, embodied, stateful, and operational.

That means combining:
- a lightweight desktop character/presence layer
- a real voice input/output layer
- an auditable agent runtime
- a memory system that separates working memory from long-term user modeling
- a safe desktop automation layer for Windows

## Repository status
This repository currently defines the product philosophy and system architecture for the first serious version.

## Documents
- [`docs/philosophy.md`](docs/philosophy.md)
- [`docs/architecture.md`](docs/architecture.md)
- [`docs/roadmap.md`](docs/roadmap.md)

## Why this project is interesting
Unlike a normal assistant app, this system aims to combine:
- **presence** — always-there, low-friction interaction
- **agency** — ability to act on the computer
- **memory** — awareness of recent context and learned habits
- **personality** — an abstract but coherent companion layer
- **safety** — explicit confirmations, scoped permissions, event history, and recoverable execution

## Long-term goal
Build a Windows desktop AI companion that feels alive enough to stay on screen, useful enough to trust with real tasks, and structured enough to inspect, constrain, and improve over time.
