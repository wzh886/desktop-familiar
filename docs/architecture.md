# System Architecture

## Top-level structure
The system should be designed as five cooperating layers:

```text
┌──────────────────────────────────────────────┐
│ 1. Embodiment Layer                          │
│    character, presence, animation, status    │
├──────────────────────────────────────────────┤
│ 2. Interaction Layer                         │
│    microphone, STT, TTS, text, confirmations │
├──────────────────────────────────────────────┤
│ 3. Agent Runtime Layer                       │
│    intent, planning, execution, supervision  │
├──────────────────────────────────────────────┤
│ 4. Memory Layer                              │
│    working, episodic, preference memory      │
├──────────────────────────────────────────────┤
│ 5. Windows Action Layer                      │
│    apps, files, browser, UI automation       │
└──────────────────────────────────────────────┘
```

---

## 1. Embodiment Layer
### Responsibility
Present the assistant as a lightweight persistent companion on the desktop.

### Responsibilities
- render the companion UI
- expose states such as listening / thinking / executing / waiting / failed
- display compact task summaries or confirmation prompts
- provide minimal but expressive visual feedback

### Candidate implementations
- Tauri + WebView UI
- Electron + front-end UI
- Godot or Unity if richer animation becomes important later

### Initial recommendation
Start with **Tauri** if speed and system integration matter more than animation depth.

---

## 2. Interaction Layer
### Responsibility
Handle all user-facing input/output flows.

### Inputs
- microphone capture
- optional wake-word or push-to-talk
- text fallback input
- hotkeys / tray menu / compact command palette

### Outputs
- speech synthesis
- on-screen bubbles / notifications
- status indicators
- approval prompts

### Internal modules
- audio capture
- STT adapter
- TTS adapter
- interrupt manager
- confirmation manager

### Key constraint
The system must support interruption gracefully. A desktop assistant that cannot be interrupted feels unusable.

---

## 3. Agent Runtime Layer
### Responsibility
Interpret intent, plan actions, choose tools, supervise execution, and emit inspectable events.

### Internal modules
#### Intent layer
- parse user request
- detect whether request is informational, operational, or conversational

#### Planner
- decompose multi-step tasks
- determine whether confirmation is required
- choose execution path

#### Runtime core
- maintain explicit task state
- supervise sub-steps / worker modules
- classify failures
- coordinate retries or escalation

#### Event system
Emit structured events such as:
- `input.received`
- `intent.classified`
- `task.created`
- `state.changed`
- `action.started`
- `action.succeeded`
- `action.failed`
- `confirmation.required`
- `memory.updated`

### Design requirement
This layer should be auditable.
The assistant must not behave like a monolithic prompt black box.

---

## 4. Memory Layer
### Responsibility
Store and retrieve recent context, meaningful episodes, and stable user preferences.

### Memory partitions
#### Working memory
- active task
- recent commands
- current app/window/file context
- recent dialogue turns

#### Episodic memory
- significant actions taken today
- recurring workflows
- interrupted task chains

#### Preference memory
- preferred apps
- naming conventions
- preferred confirmation style
- work habits and recurring routines

### Design requirement
Memory should be:
- inspectable
- editable
- scoped
- deletable
- privacy-aware

### Recommended storage
- local SQLite for v0.1
- structured tables + lightweight summaries
- optional vector retrieval later for richer semantic recall

---

## 5. Windows Action Layer
### Responsibility
Actually operate the computer.

### Action domains
- application launching/focus/switching
- file and folder operations
- browser automation
- clipboard access
- keyboard/mouse automation
- window management
- screenshots / OCR / contextual perception
- PowerShell / shell execution with policy boundaries

### Action safety classes
#### Class A — low risk
- open app
- switch window
- read title / read current state
- screenshot / inspect

#### Class B — moderate risk
- type text
- create files
- move files
- browser form interaction

#### Class C — high risk
- delete / overwrite
- send messages externally
- run shell commands with side effects
- install/uninstall software

#### Class D — restricted by default
- security-sensitive configuration changes
- credential / secret manipulation
- destructive bulk actions

### Requirement
All actions must be policy-filtered before execution.

---

## Safety and control plane
The assistant should include a policy/control layer that decides:
- what can run automatically
- what requires lightweight confirmation
- what requires explicit approval
- what is disabled entirely

### Audit data per action
- request id
- initiating user intent
- chosen action
- target resource
- result
- error if any
- confirmation record if applicable

---

## Suggested v0.1 stack
### UI shell
- Tauri

### Runtime
- Python service process

### Memory
- SQLite

### Windows automation
- PowerShell + UI Automation wrappers + safe desktop control adapters

### Speech
- Whisper-compatible STT path
- local or cloud TTS path

### Why this split
- Tauri gives a practical Windows shell
- Python gives fastest AI/runtime iteration
- SQLite keeps memory simple and local
- automation adapters can evolve independently of the runtime logic

---

## Proposed repository split
```text
desktop-familiar/
├── README.md
├── docs/
│   ├── philosophy.md
│   ├── architecture.md
│   ├── memory-model.md
│   ├── safety-model.md
│   └── roadmap.md
├── app/
│   └── tauri-shell/
├── runtime/
│   ├── core/
│   ├── memory/
│   ├── policies/
│   ├── actions/
│   └── speech/
├── examples/
└── assets/
```

---

## v0.1 milestone
### Goal
A usable local prototype, not yet a polished consumer app.

### Must-have
- desktop shell with visible assistant state
- push-to-talk voice input
- STT -> intent classification -> task execution loop
- a few safe Windows actions
- working memory over current session
- explicit confirmation for medium/high-risk actions
- action/event log visible in UI or local file

### Example demo flow
1. user says: "open VS Code and the folder I was just using"
2. assistant resolves recent folder from working memory
3. assistant asks for confirmation if ambiguity exists
4. assistant launches/focuses VS Code
5. assistant logs what it did
6. assistant remains available for follow-up

---

## Long-term direction
The project should evolve from:
- desktop companion demo

to:
- dependable personal Windows agent runtime with memory, supervision, and safe execution

That is the real ambition.
