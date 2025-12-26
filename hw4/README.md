# Introduction

This folder contains a custom multilevel memory allocator (a simple `malloc`/`free` implementation) and a small test driver for an operating systems assignment. The allocator implements fixed-size header blocks, free lists by size class, splitting and coalescing, and uses `mmap` for the backing memory.

# Overview

- `hw4_110612117.c` implements a multilevel allocator with: aligned allocation sizes, free lists per size class, block splitting, and merging adjacent free blocks on `free`.
- `main.c` is a simple test driver that reads commands from `test.txt` to allocate and free blocks and finally prints free-list information by calling `malloc(0)`.
- The allocator is intended to replace the standard `malloc`/`free` within the test program (the source defines `malloc`/`free`).

# Main Source Files

- `hw4_110612117.c`: multilevel allocator implementation. Key behaviors include:
  - Uses `mmap` to allocate a contiguous region for the allocator's heap.
  - Rounds requests to 32-byte-aligned chunks and places blocks into size-class free lists.
  - On allocation, searches for a best-fit block at or above the target size, splits if necessary, and updates linked lists.
  - On free, coalesces with adjacent free blocks and returns them to the appropriate free list.
- `main.c`: test driver that reads `test.txt` commands to allocate (`A <id> <size>`) and deallocate (`D <id>`), then calls `malloc(0)` to print free information.

# How to build

Build in a POSIX environment (WSL, Linux, macOS). Example using `gcc`:

```bash
cd hw4
gcc -std=c11 -o hw4_test main.c hw4_110612117.c
```

This produces an executable `hw4_test` which links `main.c` (the driver) with the custom allocator so the program uses the assignment's `malloc`/`free`.

# How to run

Prepare a `test.txt` containing lines like `A\t<id>\t<size>` to allocate and `D\t<id>` to free. Then run:

```bash
./hw4_test
```

The program will execute the commands and print allocator diagnostics when `malloc(0)` is called at the end.

# Examples

- Example `test.txt` lines:
  - `A\t0\t100`  — allocate 100 bytes into slot 0
  - `A\t1\t200`  — allocate 200 bytes into slot 1
  - `D\t0`        — free slot 0

- After the sequence the program calls `malloc(0)` to print the largest free chunk size and other diagnostics.

# Notes & Constraints

- Development and testing were performed inside Windows Subsystem for Linux (WSL). Build and run instructions assume a POSIX environment.
- The custom allocator uses POSIX APIs (`mmap`, `write`, etc.) and therefore requires a POSIX environment; it will not run on native Windows without compatibility layers.
- The author intends to upload only compiled executables (not source files) to any remote repository. Do not publish the original source files to public servers unless you have explicit permission.

# Files in this folder

- `multilevelBF.so` — executable of the multilevel memory allocator.
- `main` — small test driver that exercises the allocator using `test.txt` commands.
- `README.md` — this file.
- `test.txt` — example input commands for the test driver.

# License / Redistribution

- - Contact the author to request access to the original source code.
