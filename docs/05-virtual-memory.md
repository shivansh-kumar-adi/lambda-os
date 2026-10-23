# 05. Virtual memory

## Four-level paging

![Page-table walk](../assets/diagrams/page-table-walk.png)

x86-64 translates a virtual address through four table levels. Each level is indexed by nine bits of the address, and the final twelve bits are the offset inside a 4 KiB page. The root of the hierarchy is held in CR3.

| Concept | Why it matters |
|---|---|
| Canonical addresses | The upper bits must match the top valid bit. Non-canonical addresses are invalid |
| CR3 | Identifies the active top-level table |
| HHDM | The bootloader maps all physical memory at a fixed virtual offset. This is how the kernel can read table pages without assuming identity mapping |
| Physical address width | Limits which physical addresses an entry can hold |
| NX | A per-entry no-execute bit, honored only when the CPU feature is enabled |
| Large pages | A higher-level entry can map a 2 MiB or 1 GiB region directly |
| Effective permissions | The final permission is the combination across all levels, so one restrictive level wins |

## Read-only inspection (slice 0K, reported)

The inspector walks the active tables, reports the present, write, user and no-execute state at each level, and computes effective permissions. Runtime observations of the HHDM and active CR3 are reported, along with inspection of the kernel, stack and IST mappings.

## Owned page-table construction (slice 0L, reported experimental)

![Mapping lifecycle](../assets/diagrams/owned-mapping-lifecycle.png)

| Property | Behavior |
|---|---|
| Separate hierarchy | The mapper owns its own tables and never edits the active ones |
| 4 KiB mappings | Controlled page-sized mappings |
| Validation | Rejects non-canonical, misaligned and duplicate mappings |
| W^X | Rejects mappings that are both writable and executable |
| Rollback | A partial failure undoes what it built |
| Ownership | Only pages the mapper allocated are ever recycled |
| Unmapping | Supported, with safe recycling of owned table pages |
| Test modes | Seven reported QEMU modes |

## Verification levels

![Verification levels](../assets/diagrams/verification-levels.png)

| Level | Meaning | State |
|---|---|---|
| 1. Constructed | The table data exists in memory | Reported |
| 2. Software-checked | A walker reads the tables and agrees | Reported |
| 3. Loaded into CR3 | The CPU actually uses the hierarchy | **Not done** |
| 4. CPU access through it | Reads and writes through the mappings succeed | **Not done** |
| 5. Hardware NX fault | Executing a no-execute page faults | **Not done** |
| 6. TLB lifecycle | Invalidation is correct on a live address space | **Not done** |

These are deliberately kept apart. A correct-looking table is not proof that the CPU will enforce it.

## Why the hierarchy is inactive

Activating a wrong hierarchy can destroy the running kernel instantly, with no way to report why. Keeping it inactive while the builder and validator are proven is the safer order. Safe activation is the next milestone.
