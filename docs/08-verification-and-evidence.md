# 08. Verification and evidence

## How kernel tests work

![QEMU test flow](../assets/diagrams/qemu-test-flow.png)

1. The kernel and a bootable ISO are built.
2. QEMU boots the ISO for a bounded amount of time.
3. Serial output is captured to a log.
4. The log is checked for the expected markers.

## Pass and fail

| Situation | Verdict |
|---|---|
| Expected markers present, run ended by time limit because the kernel halts by design | Pass |
| Run ended by time limit, markers missing | Fail |
| Crash, reset or early exit | Fail |

An expected timeout is a way to stop a kernel that halts on purpose. It is not evidence by itself. The serial markers decide.

## Reported test coverage

| Area | Reported QEMU check |
|---|---|
| Boot | Normal kernel boot and serial banner |
| Exceptions | Controlled divide-by-zero and invalid-opcode |
| Double fault | Delivery on the dedicated IST stack |
| Physical memory | Allocation integration tests and rejection of unsafe overlaps |
| Virtual memory | Page-table inspection, kernel, stack and IST mappings |
| Owned mapper | Seven reported test modes for mapping, validation, rollback and unmapping |

## Artifact integrity

Build outputs (kernel image and ISO) can be hashed so a result can be tied to an exact build. Hashes are specific to one build, so they are recorded alongside the log they belong to and are never reused for later builds.

## Evidence still to publish

| Evidence | Status |
|---|---|
| Serial logs for each test mode | To be collected |
| Build and test duration | Not yet recorded for publication |
| Kernel image size | Not yet recorded for publication |
| Desktop screenshots | To be collected |

No benchmark or measurement is presented without a recorded source.

## Limits of this evidence

All kernel testing is under QEMU. Real hardware behavior, especially around paging and the TLB, has not been verified. The checkpoints are author-reported, and they are not a substitute for re-running the tests on the current commit.
