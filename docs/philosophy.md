# Philosophy

## 1. The assistant should not live only inside a chat box
Conventional AI products assume the right interface is a text conversation.
That is convenient for deployment, but weak for daily use.
A personal agent that is meant to stay with someone throughout the day should feel:
- present
- interruptible
- ambient
- low-friction
- situated in the user's real working environment

A desktop companion satisfies this better than a pure chat window.

---

## 2. "Desktop pet" is the aesthetic shell, not the product definition
A desktop pet without real utility is novelty.
An automation tool without presence is cold and forgettable.
The project aims to combine the two.

The visual companion layer exists to:
- reduce psychological distance
- lower interaction cost
- provide status without demanding focus
- create continuity of presence across tasks

The real product is a **personal agent shell**.

---

## 3. Memory should be layered, not blobbed
Most AI memory implementations fail because they collapse all memory into one undifferentiated context bucket.
This project should distinguish:

### Working memory
- what the user is doing right now
- current task state
- recent commands
- recent windows/apps/files/events

### Episodic memory
- what happened today or recently
- meaningful events or sequences
- task histories

### Preference memory
- stable user habits
- naming preferences
- favorite tools/apps
- communication style
- boundaries and sensitivities

Each layer should be editable, inspectable, and revocable.

---

## 4. Agency without inspectability is not acceptable
If the system can operate a Windows desktop, then it must not behave like a black box.
The user should be able to know:
- what it is doing
- why it is doing it
- what it just touched
- what failed
- what needs confirmation

This means the execution layer must be auditable and event-driven.
The assistant should not silently jump from intent to action without structured visibility.

---

## 5. Safety must be designed into the interaction model
The point is not just to make an agent powerful.
The point is to make it useful without making it reckless.

The project should separate actions into classes:
- safe / low-risk actions
- medium-risk actions requiring lightweight confirmation
- high-risk actions requiring explicit approval
- forbidden actions unless manually enabled

A user should never feel that the assistant is one hallucination away from damaging the machine.

---

## 6. Personality should emerge through consistency, not gimmicks
The companion should not feel like a bundle of random emotions.
Its personality should come from:
- stable tone
- repeatable behavior
- predictable task handling
- continuity of memory
- visible state changes

Abstract presence works better than forced cartoon theatrics.
The system should feel calm, coherent, and reliable.

---

## 7. The best assistant is one that understands both state and momentum
Real human work is not just a sequence of commands.
It has momentum:
- what was started
- what is currently active
- what was interrupted
- what probably matters next

The assistant should become useful not merely by answering a question, but by understanding task progression over time.

---

## 8. This is best treated as an operating layer, not a feature
The project is not just a toy on the screen.
It is closer to a personal operating layer for:
- communication with the machine
- memory over time
- task execution
- lightweight workflow continuity

That framing makes better product decisions than thinking of it as a pet with commands.

---

## Design thesis
A successful Windows AI companion should feel like:
- a visible and approachable presence
- a trustworthy execution agent
- a persistent contextual memory
- an inspectable and constrained system

Not a chatbot. Not only a pet. Not only an automation script.

A **familiar**: an ambient personal intelligence attached to the desktop.
