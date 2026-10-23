# 02. Architecture overview

## System context

![System context](../assets/diagrams/system-context.png)

ΛOS has two tracks that share goals but not a runtime:

1. **Desktop and AI workspace** (reported): a branded desktop plus an AI backend foundation with permission policies and bounded, audited operations.
2. **K1 kernel** (reported): a freestanding x86-64 kernel that boots and is tested under QEMU.

The desktop does not run on K1. A host operating system or compatibility layer is the proposed way to reach existing browsers and applications, and that choice is undecided.

## Product architecture

![Product architecture](../assets/diagrams/product-architecture.png)

### Components and responsibilities

| Component | Responsibility | Status |
|---|---|---|
| Desktop shell | Windows, visual identity, overall experience | Reported |
| Dock | Application and workspace access | Reported |
| Launcher | Finding and starting things | Reported |
| Settings | Configuration | Reported |
| AI assistant surface | Conversation and results inside the desktop | Reported |
| AI backend | Request handling, provider integration, tool selection | Reported foundation |
| Permission policy | Allow or deny a tool call | Reported |
| Bounded operations | Keep operations inside limits | Reported |
| Audit record | Record attempts and outcomes | Reported |
| System interfaces | The real OS surface the assistant could act on | Undecided |
| K1 kernel | Experimental kernel | Reported, separate |

## Trust boundaries

- **User to desktop.** The user supplies requests and approvals.
- **Desktop to AI backend.** Requests cross from the interface into the service that holds provider access.
- **AI backend to permission policy.** Every tool call must be judged before it acts.
- **Policy to system interfaces.** The only path from the assistant to the machine should pass through this boundary.

Where the boundaries sit in code, and how complete the coverage is, are not published in this showcase. See [AI security model](06-ai-security-model.md).

## Integration status

| Relationship | Status |
|---|---|
| Desktop to AI backend | Reported |
| AI backend to permission and audit | Reported |
| Desktop on K1 | Not integrated |
| Desktop on a Linux base | Proposed, undecided |
| Existing browsers and applications | Planned, depends on platform |

Dashed lines in the diagrams mark anything proposed or unverified.
