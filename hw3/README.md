# Introduction

This folder contains a multi-threaded sorting implementation (assignment 3) written in C++ that demonstrates dividing data into chunks, local sorting (bubble sort), and parallel merging using POSIX threads and semaphores.

# Overview

- Splits input data into chunks and sorts each chunk with bubble sort.
- Uses multiple worker threads to perform sorting and merging tasks concurrently.
- Synchronization is managed with three semaphores (task availability, task completion, and a mutex-like semaphore).
- Produces sorted output files named `output_<thread_count>.txt` and prints elapsed time per thread count.

# Main Source File

- `hw3_110612117.cpp`: primary implementation. Key behaviors:
  - Reads `input.txt`, which begins with the number of elements followed by the elements.
  - Divides data into chunks and enqueues sorting tasks for worker threads.
  - Uses semaphores and a task queue to coordinate sorting and merging operations.
  - Writes sorted results to `output_<thread_count>.txt` for each tested thread count.

# How to build

Compile on a POSIX-compatible environment with pthreads support (Linux, WSL, macOS). Example using `g++`:

```bash
g++ -std=c++11 -pthread -o parallel_sort hw3_110612117.cpp
```

# How to run

Prepare an `input.txt` where the first number is the count N followed by N integers. Then run:

```bash
./parallel_sort
```

The program will run tests with varying worker thread counts (1..max) and produce `output_1.txt`, `output_2.txt`, etc.

# Examples

- To generate a simple decreasing sequence for testing, the code includes a helper to create `input.txt` (used in `test_mode`).
- After running, verify `output_<n>.txt` files are sorted.

# Notes & Constraints

- Development and testing were performed inside Windows Subsystem for Linux (WSL). Build and run instructions assume a POSIX environment.
- The program depends on POSIX threads and semaphores (`pthread`, `sem_t`) and therefore requires a POSIX environment; it will not compile or run on native Windows without compatibility layers.
- The author intends to upload only compiled executables (not source files) to any remote repository. Do not publish the original source files to public servers unless you have explicit permission.

# Files in this folder

- `parallel_sort` — executable of the parallel sorting assignment.
- `README.md` — this file.

# License / Redistribution

- - Contact the author to request access to the original source code.
