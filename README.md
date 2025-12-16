# Minishell

[![C](https://img.shields.io/badge/language-C-555?style=flat-square&logo=c)](https://www.gnu.org/software/gnu-c-manual/)]
[![License](https://img.shields.io/badge/license-Educational-lightgrey?style=flat-square)]
A minimal Unix shell written in C, focusing on low-level system programming and Unix process management.

This project reproduces a subset of Bash behavior, including command execution, pipelines, redirections, environment handling, and heredocs, with careful attention to memory management and signals.

---

## Technical Overview

### Features

- Command execution using `fork`, `execve`, and `wait`
- Pipes (`|`)
- Redirections (`<`, `>`, `>>`)
- Heredocs (`<<`) with proper delimiter handling and variable expansion
- Environment variables (`export`, `unset`, `$VAR`)
- Wildcard expansion (`*`)
- Built-in commands:
  - `cd`
  - `echo`
  - `pwd`
  - `env`
  - `export`
  - `unset`
  - `exit`
- Subshells
- Command history (via `readline`)
- Accurate exit status handling (`$?`)
- Robust signal handling (`Ctrl-C`, `Ctrl-\`) in interactive mode, heredocs, and execution

### Architecture

Minishell is built as a multi-stage execution pipeline:

- Lexer : `Tokenizes user input and builds execution structures`
- Parser : `Analyses syntax correctness`
- Expansion : `Manages environment variables and expansion`
- Execution : `Handles command execution, pipelines, redirections, subshells, and process management`
  
- Heredoc Handling : `Dedicated logic for heredoc parsing, expansion, and signal safety`
- Signal Handling : `Context-aware signal management for interactive prompt / heredocs / child processes`

### Memory Management

- No memory leaks in project code (verified with Valgrind)
- The readline library introduces known, unavoidable allocations; these are ignored using a Valgrind suppression file when checking for leaks

---

## Build & Run

### Requirements
- Unix-like system
- `readline` library

### Install readline :

- On Linux:
`sudo apt install libreadline-dev`
- On macOS:
`brew install readline`

### Compilation
`make`

### Run
`./minishell`

---

## More

### Collaboration

This project was developed collaboratively by :
-Theo Fiette - tfiette
-Alyssia Galleze - agalleze

### Educational Context

This project was developed as part of a systems programming curriculum and aims to demonstrate:
- Strong understanding of Unix process model
- Careful file descriptor and signal management
- Robust error handling
- Clean architecture and maintainable C code

This project is for educational purposes.
It is not intended to be a full Bash replacement, but an educational reimplementation focused on correctness, clarity, and low-level behavior.
