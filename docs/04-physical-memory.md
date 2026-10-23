# 04. Physical memory

## Pipeline

![Memory-map pipeline](../assets/diagrams/memory-map-pipeline.png)

## Problem

The kernel learns what memory exists from the bootloader's memory map. That map is firmware-derived input. If the kernel hands out a page that is reserved, belongs to the kernel itself, or is described twice, the result is silent corruption that appears much later and far from the cause.

## Approach (reported)

| Concern | Handling |
|---|---|
| Reserved ranges | Treated as off limits |
| The kernel's own physical range | Explicitly excluded |
| Page alignment | Regions are aligned to page boundaries |
| Region normalization | Regions are put into a consistent, ordered form |
| Overlap | Unsafe overlapping or malformed entries are rejected rather than repaired by guessing |
| Bootloader-reclaimable memory | Treated carefully, since the bootloader's own data may still be in use |
| Metadata | The allocator keeps its own bookkeeping for free and used pages |
| Failure | Allocation failure is reported, not hidden |

## Verification

Allocation integration tests under QEMU are reported. Any memory figures observed during a test run are observations about that run, not guarantees. They are not repeated here because they depend on the QEMU memory setting used.

## Limitations

- Physical page granularity only. There is no kernel heap yet.
- Memory capacity is bounded by the design of the allocator's metadata.
- Behavior on very different physical memory layouts has not been broadly tested.
