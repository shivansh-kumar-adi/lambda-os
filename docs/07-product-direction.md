# 07. Product direction: Linux, hybrid or custom?

![Architecture options](../assets/diagrams/architecture-options.png)

## The constraint

The desired experience includes Chrome, Edge, Firefox and ordinary applications, without building a new browser or an app store. Those programs depend on a mature operating system underneath. Booting a custom kernel does not provide that.

## Options

### A. Linux-based ΛOS
Use an existing Linux kernel and system infrastructure and build the distinctive desktop and AI layer on top. Existing drivers, filesystems, networking, browsers and package ecosystems come with it. K1 would no longer be the product foundation.

### B. Hybrid
A usable ΛOS desktop on a Linux base, with the custom desktop and AI integration layer on top, while K1 continues as a separate experimental kernel track. The tracks share design goals and documentation without pretending to share a kernel.

### C. Fully custom K1 foundation
K1 becomes the base of the final product. That requires hardware drivers, networking, storage, a filesystem, process isolation, system calls, application loading, graphics, audio, security, recovery and updates, plus a way to run browsers and existing applications.

## Comparison

| Criterion | A. Linux | B. Hybrid | C. Custom K1 |
|---|---|---|---|
| Time to a usable desktop | Shortest | Short | Very long |
| Engineering difficulty | Moderate | Moderate, split across two tracks | Very high |
| Software compatibility | Strong | Strong on the product track | Weak until a compatibility layer exists |
| Hardware support | Strong | Strong on the product track | Minimal |
| Security and maintenance | Inherits a mature base | Mature base plus an experimental track | Everything is owned by one developer |
| Fit for a solo student developer | Good | Good, with discipline | Poor for a full product |
| Long-term originality | Lower at the kernel level | High at the desktop and AI level, plus K1 | Highest |
| Portfolio and learning value | Good | Highest overall | High, but risk of an unfinished product |

## Recommendation (not a decision)

Option B best matches the stated goals: it respects the decision to use established browsers and applications, it delivers a usable product sooner, and it preserves the kernel work as a deep systems-engineering track. This is a recommendation. No migration has been done, the repository direction has not changed, and the choice remains an **open decision** for the project owner.

## Rules that hold regardless

- The desktop is never described as running on K1 unless that is demonstrated and verified.
- No compatibility with any browser or application is claimed without evidence.
- No custom app store is claimed.
