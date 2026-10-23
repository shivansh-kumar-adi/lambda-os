# 11. Known limitations and open decisions

## Limitations

| Area | Limitation |
|---|---|
| Integration | The desktop does not run on K1 |
| Address spaces | The owned hierarchy is inactive and has never been loaded into CR3 |
| Hardware NX | No NX fault has been demonstrated through the owned mappings |
| TLB | Invalidation on an active address space is unvalidated |
| Memory | No kernel heap |
| CPU services | No interrupts or timers beyond exception handling |
| Multitasking | No scheduler |
| Isolation | No system calls and no userspace |
| Platform | No storage, filesystem, device support, graphics or networking |
| Hardware | Tested under QEMU only |
| Compatibility | No verified compatibility with existing browsers or applications |
| AI security | Full coverage of routes and tools by policy is not claimed; no external audit |
| Evidence | Screenshots and recorded logs are still being collected |

## Open decisions

| Decision | State |
|---|---|
| Linux, hybrid or custom foundation for the product | Open. Hybrid is recommended, not chosen |
| Which host platform or compatibility layer provides browsers and applications | Open |
| How the AI workspace reaches real system interfaces | Depends on the platform decision |
| Release format and distribution | Open |
| Source publication | Not published while the project is in active development |
