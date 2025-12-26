# Introduction

This folder contains a parallel matrix multiplication implementation in C++ for an operating systems assignment. The program demonstrates using multiple processes and System V shared memory to distribute work and measure elapsed time.

# Overview

- Implements matrix multiplication using multiple processes (forked children).
- Uses System V shared memory (`shmget`, `shmat`, `shmctl`) to share matrices and checksum between processes.
- Divides work by rows among processes and aggregates a checksum from partial results.
- Measures elapsed wall-clock time for each tested number of processes.

# Main Source File

- `110612117_hw2.cpp`: primary implementation. Key behaviors:
  - Reads an integer `parameter` (matrix dimension) from standard input.
  - Allocates shared memory to store `matrixA`, `matrixB`, `matrixC`, and a shared checksum.
  - Forks up to `process_number` (16) processes; each child computes a portion of the product.
  - Parent waits for all children and reports elapsed time and the aggregated checksum.

# How to build

Compile with a POSIX-compatible C++ compiler (Linux, WSL, or macOS). Example using `g++`:

```bash
g++ -std=c++11 -o matrix_mul 110612117_hw2.cpp
```

# How to run

Provide the matrix dimension as input (program reads from stdin). Example:

```bash
echo 512 | ./matrix_mul
```

Or run interactively and type a number when prompted:

```bash
./matrix_mul
1024
```

# Examples

- The program iterates `pnum` from 1 to 16 processes and prints elapsed time and checksum for each.
- Use reasonable matrix sizes to avoid running out of memory (e.g., 256, 512). Shared memory size grows with parameter^2.

# Notes & Constraints

- Development and testing were performed inside Windows Subsystem for Linux (WSL). Build and run instructions assume a POSIX environment.
- The author intends to upload only compiled executables (not source files) to any remote repository. Do not publish the original source files to public servers unless you have explicit permission.
- This program relies on POSIX APIs and System V IPC; it requires a POSIX environment (Linux, WSL, macOS). It will not compile or run on native Windows without compatibility layers.
- Shared memory segments are removed (`IPC_RMID`) after use in the program, but if the program aborts unexpectedly a segment may remain — check with `ipcs` and remove with `ipcrm` if necessary.

# Files in this folder

- `matrix_mul` — executable of the parallel matrix multiplication.
- `README.md` — this file.

# License / Redistribution

- - Contact the author to request access to the original source code.
