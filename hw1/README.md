# Introduction

This repository contains a simple UNIX-like shell implementation written in C++ for an operating systems assignment. The main program implements basic command parsing, piping, input/output redirection, background execution, and child process management.

# Overview

- Implemented a minimal interactive shell that reads commands from standard input and executes them.
- Supports pipelines using the `|` operator (e.g., `ls | grep txt`).
- Supports input (`<`) and output (`>`) redirection for individual commands.
- Supports background execution with `&` at the end of a command line.
- Installs a `SIGCHLD` handler to reap child processes and avoid zombies.

# Main Source File

- `110612117_hw1.cpp`: the primary implementation of the shell. Key behaviors include:
  - Parsing the command line into a sequence of `Command` objects (arguments, input_file, output_file).
  - Creating pipes between commands when multiple stages are present.
  - Forking child processes and using `execvp` to run external programs.
  - Using `dup2` to redirect stdin/stdout for pipes and file redirection.
  - Handling background jobs (when the command line ends with `&`) so the shell does not wait.

# How to build

Compile the C++ source with a POSIX-compatible compiler (Linux/macOS). Example using `g++`:

```bash
g++ -std=c++11 -o simple_shell 110612117_hw1.cpp
```

# How to run

After building, run the produced executable and type commands at the prompt:

```bash
./simple_shell
>
```

Examples:
- Run a pipeline: `ls -l | grep .cpp`
- Redirect input: `sort < input.txt`
- Redirect output: `echo hello > out.txt`
- Background execution: `sleep 5 &`

# Notes & Constraints

- Development and testing were performed inside Windows Subsystem for Linux (WSL). Build and run instructions assume a POSIX environment.
- The author intends to upload only compiled executables (not source files) to any remote repository. Do not publish the original source files to public servers unless you have explicit permission.
- This program uses POSIX APIs (`fork`, `execvp`, `pipe`, `dup2`, `sigaction`) and therefore requires a POSIX environment to compile and run (e.g., Linux, WSL, macOS). It will not compile as-is on native Windows without a POSIX compatibility layer.
- The source header includes a student statement noting that the program should not be posted to a public server (e.g., a public GitHub repository). Please respect that constraint when sharing or distributing the code.

# Files in this folder

- `simple_shell` — executable of the simple shell.
- `README.md` — this file.

# License / Redistribution

- Contact the author to request access to the original source code.
