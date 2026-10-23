# Diagram guide

Every diagram has a Mermaid source (`.mmd`) in this folder and rendered SVG and PNG copies in `../../assets/diagrams/`. Solid boxes are reported components. Dashed boxes and lines are planned, proposed or unverified.

| Diagram | Source | What it shows |
|---|---|---|
| System context | `system-context.mmd` | The two tracks and the proposed host layer |
| Product architecture | `product-architecture.mmd` | Desktop, AI backend, trust boundary, K1 |
| AI permission and audit flow | `ai-permission-audit-flow.mmd` | Allowed and denied paths |
| K1 boot sequence | `k1-boot-sequence.mmd` | Firmware to halt |
| K1 subsystem layers | `k1-subsystem-layers.mmd` | Kernel layers |
| Exception handling flow | `exception-handling-flow.mmd` | Fault to controlled halt, with the IST path |
| GDT, TSS, IST | `gdt-tss-ist.mmd` | How the double-fault stack is reached |
| Memory-map pipeline | `memory-map-pipeline.mmd` | From firmware map to allocator |
| Page-table walk | `page-table-walk.mmd` | Four-level translation |
| Owned mapping lifecycle | `owned-mapping-lifecycle.mmd` | Validate, build, roll back, unmap |
| Verification levels | `verification-levels.mmd` | What is and is not proven |
| QEMU test flow | `qemu-test-flow.mmd` | How tests decide pass or fail |
| Architecture options | `architecture-options.mmd` | Linux, hybrid, custom |
| Milestone dependencies | `k1-milestone-dependencies.mmd` | Kernel roadmap order |
| Development timeline | `development-timeline.mmd` | Slices 0G to 0L |

To re-render a diagram, use Mermaid CLI with the neutral theme and a white background.
