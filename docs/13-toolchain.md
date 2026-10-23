# 13. Toolchain

This is a high-level description of the reported development environment. It is not an installation guide, and it contains no machine-specific paths.

| Tool | Role |
|---|---|
| MSYS2 | Development environment, in a dedicated toolchain root separate from an older MSYS2 install |
| Clang | Compiles the freestanding kernel |
| LLVM/LLD | Links the kernel using a linker script |
| GNU Make | Orchestrates builds |
| QEMU | Boots and tests the kernel under emulation |
| xorriso | Creates the bootable ISO |
| Limine | Bootloader, v12.9.1 assets, with signature verification reported successful |

## Notes

- The kernel is built freestanding. There is no operating system or standard C runtime beneath it.
- A pinned copy of the Limine protocol header keeps the kernel consistent with the bootloader assets.
- Separating the toolchain from an older MSYS2 install avoids version and path conflicts.
- Build and run commands belong in the private source repository. They are not reproduced here because this showcase does not publish the source tree.
