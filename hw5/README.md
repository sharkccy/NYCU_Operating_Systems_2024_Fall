# Introduction

This folder contains the advanced page-replacement simulator for an operating systems assignment. The simulator implements LRU and a Clean-First LRU (CFLRU) variant using separate regions to reduce write-backs.

# Overview

- The program parses a memory-access trace (operations `R`/`W` and hex addresses) and reports hits, misses, page-fault ratio, and write-back counts for several frame sizes.
- This README documents the complex/primary implementation only; a simpler variant exists in the workspace for experimentation but will not be uploaded or published.

# Main Source File

- `hw5_110612117.cpp`: advanced CFLRU implementation. Key features:
  - Maintains three lists: `cleanFirstList`, `workingList`, and `cleanList` to implement a clean-first region and a working region.
  - Uses lightweight hash tables for O(1) page lookups and region membership checks.
  - Eviction policy prioritizes removing clean pages from the clean-first region when available to reduce write-backs; otherwise evicts from working region and counts write-backs.

# How to build

Build in a POSIX environment (WSL, Linux, macOS). Example using `g++` with optimization:

```bash
cd hw5
g++ -std=c++11 -O2 -o LRU_CFLRU hw5_110612117.cpp
```

# How to run

The executable accepts a single argument: the trace file path. Example:

```bash
./hw5_adv trace.txt
```

Output: per-frame statistics (`Frame`, `Hit`, `Miss`, `Page fault ratio`, `Write back count`) and elapsed times for LRU and CFLRU.


# Notes & Constraints

- Development and testing were performed inside Windows Subsystem for Linux (WSL). Build and run instructions assume a POSIX environment.
- The program depends on C++ STL containers and POSIX timing (`gettimeofday`); native Windows may require WSL or another POSIX compatibility layer.
- The author will upload only the compiled executable; the simplified variant and original source files should not be published publicly without permission.

# Files in this folder

- `LRU_CFLRU` — executable of the page-replacement simulator.
- `README.md` — this file.
-  `text.txt` — example trace file for testing.

# License / Redistribution

- The author will only upload compiled executables for distribution. Contact the author to request access to the original source code and for permission before sharing it publicly.
