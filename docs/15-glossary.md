# 15. Glossary

| Term | Meaning |
|---|---|
| ΛOS | The project: LambdaOS |
| K1 | The custom x86-64 kernel track |
| Slice | A small, tested increment of kernel work (0G to 0L so far) |
| Limine | The bootloader and its boot protocol |
| HHDM | Higher-half direct map: all physical memory mapped at a fixed virtual offset |
| IDT | Interrupt Descriptor Table: maps exception vectors to handlers |
| GDT | Global Descriptor Table: segment descriptors |
| TSS | Task State Segment: holds the Ring 0 stack pointer and IST entries |
| IST | Interrupt Stack Table: dedicated stacks for chosen exceptions |
| Double fault | A fault raised while handling another fault, often a sign of a broken stack |
| CR3 | Register holding the physical address of the top-level page table |
| PML4 | Top-level page table |
| TLB | Cache of address translations |
| NX | No-execute permission bit |
| W^X | Rule that a page is never both writable and executable |
| Canonical address | A 64-bit address whose unused upper bits match the top valid bit |
| QEMU | Emulator used to boot and test the kernel |
| Serial | Text output channel used for kernel diagnostics |
| Audit | A record of an attempted or performed action |
| Bounded operation | An operation that runs inside explicit limits |
