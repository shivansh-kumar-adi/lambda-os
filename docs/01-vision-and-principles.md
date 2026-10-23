# 01. Vision and principles

![ΛOS logo](../assets/brand/lambdaos-logo.png)

## The vision

ΛOS aims to be a distinctive, developer-oriented computing experience that brings together:

- a polished desktop with its own identity and workflow,
- familiar browsers and ordinary applications,
- an AI assistant that works with system capabilities through controlled interfaces,
- security-conscious, auditable automation,
- and a real understanding of operating-system internals.

It should feel like one coherent system rather than a pile of unrelated applications.

## Explicit product decisions

| Decision | Meaning |
|---|---|
| Existing browsers, not a homegrown browser | Chrome, Edge and Firefox are the intended experience. No new browser engine is planned. |
| Existing applications, not a proprietary app store | Established software distribution is preferred wherever the platform allows it. No custom app store is claimed or planned. |
| K1 is a separate engineering track | The custom kernel is documented on its own merits. It is not presented as powering the desktop. |
| No silent architecture change | The Linux, hybrid and custom-kernel question is recorded as open. See [Product direction](07-product-direction.md). |

Browsers and applications have platform-specific dependencies. A kernel that boots does not automatically run them.

## Why a custom kernel at all?

Building K1 is a learning and engineering effort. It forces exact answers to questions that higher layers can ignore: how a machine boots, how the CPU reports faults, how memory is discovered, protected and reclaimed. It is a different undertaking from customizing a Linux desktop distribution, and the two are kept distinct on purpose.

## Design principles

| Principle | What it means here | Evidence level |
|---|---|---|
| Useful before flashy | Prefer working behavior over visual effect | Intent |
| Existing software where practical | Reuse established browsers and applications | Intent |
| Explicit permissions for consequential actions | AI tool calls pass a policy check | Reported in the AI backend foundation |
| Auditable operations | Actions are recorded | Reported in the AI backend foundation |
| Clear separation of concerns | Desktop, AI services and kernel are separate tracks | Reflected in the architecture |
| Small, verifiable increments | The kernel is built in slices with tests | Reflected in slices 0G to 0L |
| Failure containment | Exceptions end in controlled, reported halts | Reported in the kernel |
| Reproducible testing | Bounded QEMU runs with serial markers | Reported |
| Honest limitations | Each document lists what is missing | Applied throughout this showcase |

A principle is described as an implemented guarantee only where there is evidence for it. Otherwise it is an intention.
