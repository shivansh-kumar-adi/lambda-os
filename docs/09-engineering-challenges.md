# 09. Engineering challenges

Sixteen case studies, each written as problem, difficulty, approach, verification, trade-off and remaining limitation. All outcomes are author-reported. Where a historical account is not available it is labelled as such.

## 1. Booting a freestanding kernel in a controlled environment

- **Problem:** Get from firmware to kernel code with nothing underneath: no OS, no C runtime.
- **Why it is difficult:** Nothing can be assumed. The first instructions, the stack and the output path all have to be arranged by hand.
- **Approach:** Use the Limine protocol for handoff, a linker script for layout, and serial output for diagnostics, all run in QEMU.
- **Verification:** Normal boot test with a serial banner (slice 0G).
- **Trade-off:** Depends on a bootloader and an emulator rather than real hardware.
- **Remaining limitation:** Only QEMU is covered.

## 2. Stack alignment and CPU state during exception entry

- **Problem:** Enter C from an exception without corrupting the faulting context or the calling convention.
- **Why it is difficult:** The CPU hands over an arbitrary stack and registers, while C code assumes alignment and clobbers registers.
- **Approach:** Assembly stubs preserve registers, keep the stack aligned, and build a normalized frame before calling C.
- **Verification:** Divide-by-zero and invalid-opcode tests (slice 0H).
- **Trade-off:** More assembly to maintain.
- **Remaining limitation:** Only some exception vectors have been exercised.

## 3. Exceptions with different error-code behavior

- **Problem:** Handle vectors that push an error code and vectors that do not with one handler.
- **Why it is difficult:** The stack layout differs per vector, so a single handler would read the wrong data.
- **Approach:** Push a placeholder where the CPU pushes nothing, so every frame has the same shape.
- **Verification:** Exception tests (slice 0H).
- **Trade-off:** A small amount of per-vector stub code.
- **Remaining limitation:** Not every vector is exercised.

## 4. Recovering diagnostics from fatal exceptions

- **Problem:** Say what went wrong before stopping.
- **Why it is difficult:** After a fault the system state is untrusted, so reporting must be simple and independent of other subsystems.
- **Approach:** Print the vector, error code and instruction pointer over serial, then halt in a controlled way.
- **Verification:** Serial markers checked in the exception tests.
- **Trade-off:** No recovery, only reporting.
- **Remaining limitation:** No stack trace or symbolization is claimed.

## 5. A reliable double-fault path with a dedicated IST stack

- **Problem:** Report a fault even when the kernel stack is unusable.
- **Why it is difficult:** A fault on a broken stack cannot push its own frame, which escalates to a reset with no report.
- **Approach:** Create a kernel-owned GDT and TSS and give the double-fault gate its own stack through the IST.
- **Verification:** Double-fault delivery test (slice 0I).
- **Trade-off:** Extra memory is reserved for a stack that is rarely used.
- **Remaining limitation:** Only one dedicated stack is claimed.

## 6. Parsing memory maps without trusting overlaps

- **Problem:** Build a safe view of memory from firmware-derived data.
- **Why it is difficult:** Malformed or overlapping ranges can lead to handing out memory that is already in use.
- **Approach:** Normalize regions, align them, and reject unsafe overlaps instead of repairing them by guesswork.
- **Verification:** Allocator integration tests, including rejection of unsafe overlaps (slice 0J).
- **Trade-off:** Rejecting a map is stricter than a best-effort parse.
- **Remaining limitation:** Behavior on unusual real-hardware maps is untested.

## 7. Avoiding allocation from reserved physical memory

- **Problem:** Never return a page the kernel or firmware still needs.
- **Why it is difficult:** Reserved ranges, the kernel image and bootloader data all live in physical memory.
- **Approach:** Exclude reserved ranges and the kernel's physical range, and treat bootloader-reclaimable memory carefully.
- **Verification:** Allocation tests (slice 0J).
- **Trade-off:** Some reclaimable memory is not reused early.
- **Remaining limitation:** No broader stress testing is claimed.

## 8. Inspecting page tables without assuming identity mapping

- **Problem:** Read the active paging structures from kernel code.
- **Why it is difficult:** Table entries hold physical addresses, but the kernel runs on virtual ones.
- **Approach:** Read table pages through the HHDM provided by the bootloader.
- **Verification:** Runtime inspection observing HHDM and active CR3 (slice 0K).
- **Trade-off:** Relies on the bootloader's HHDM.
- **Remaining limitation:** Read only.

## 9. Effective permissions across multiple paging levels

- **Problem:** Compute what access a page really has.
- **Why it is difficult:** Write, user and no-execute bits at every level combine, so one restrictive level changes the result.
- **Approach:** The inspector combines permissions across levels and understands large pages.
- **Verification:** Inspection of kernel, stack and IST mappings (slice 0K).
- **Trade-off:** A software model of the hardware rules.
- **Remaining limitation:** Hardware enforcement through new mappings is not demonstrated.

## 10. Building a separate hierarchy without touching the active one

- **Problem:** Experiment with page tables safely.
- **Why it is difficult:** An error in the live tables can crash the machine instantly with no output.
- **Approach:** Build an inactive, separately owned hierarchy and do not load it into CR3 yet.
- **Verification:** Mapper test modes under QEMU (slice 0L).
- **Trade-off:** Results prove construction, not CPU behavior.
- **Remaining limitation:** Activation is not done.

## 11. Rejecting malformed mappings and writable-plus-executable permissions

- **Problem:** Stop invalid or unsafe mappings at the door.
- **Why it is difficult:** Bad mappings are easy to create and hard to notice later.
- **Approach:** Validate canonical form, alignment, duplicates and W^X before building anything.
- **Verification:** Rejection tests among the seven reported modes.
- **Trade-off:** Strict validation limits flexibility.
- **Remaining limitation:** Hardware NX enforcement is not shown.

## 12. Rolling back partial mappings without leaking or recycling unowned pages

- **Problem:** Undo a mapping that fails part way.
- **Why it is difficult:** Several levels may already have been created, and recycling a page the mapper does not own would corrupt memory.
- **Approach:** Track ownership, undo what was built, and recycle only owned pages.
- **Verification:** Rollback and recycling tests (slice 0L).
- **Trade-off:** Ownership bookkeeping adds complexity.
- **Remaining limitation:** Only tested in the inactive mapper.

## 13. Bounding QEMU tests and separating expected halts from failures

- **Problem:** Run tests that cannot hang forever, without mistaking a timeout for success.
- **Why it is difficult:** The kernel halts by design, so the emulator is ended by a time limit even when everything worked.
- **Approach:** Bound each run and decide pass or fail from the serial markers, not from how the run ended.
- **Verification:** Marker-based checks in the reported test setup.
- **Trade-off:** Tests depend on exact log markers.
- **Remaining limitation:** No real hardware testing.

## 14. Preserving work across incremental AI-assisted development

- **Problem:** Keep valuable changes safe while using AI tools to speed development.
- **Why it is difficult:** AI tools can rewrite or discard work, and their reports about what was done can be wrong.
- **Approach:** Work in small slices, record evidence, and avoid destructive version-control actions.
- **Verification:** A detailed historical account is not available for this showcase and is labelled unknown.
- **Trade-off:** Slower, more careful progress.
- **Remaining limitation:** Process claims cannot be independently verified from this repository.

## 15. Designing AI tool permissions, bounded operations and auditability

- **Problem:** Let an assistant act without giving it unlimited power.
- **Why it is difficult:** Every tool is a possible path to the machine, and an unaudited path is hard to trust.
- **Approach:** Judge each tool call with a policy, run it inside limits, and record the result.
- **Verification:** Reported as a foundation. Full coverage is not claimed.
- **Trade-off:** More friction for the assistant and for the user.
- **Remaining limitation:** No external audit and no claim of hardening.

## 16. Keeping ambition realistic: custom kernel or an existing foundation

- **Problem:** Deliver a usable product while keeping the kernel work alive.
- **Why it is difficult:** Browsers and applications depend on a mature platform that one developer cannot replace quickly.
- **Approach:** Compare Linux, hybrid and custom options and recommend hybrid, without migrating anything.
- **Verification:** Documented reasoning, see Product direction.
- **Trade-off:** Two tracks to maintain.
- **Remaining limitation:** The decision is still open.
