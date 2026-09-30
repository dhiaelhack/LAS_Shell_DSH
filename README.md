# LAS Shell

LAS Shell is a small Unix-style command-line shell written in C. It provides an interactive prompt, several built-in commands, and support for running external programs, scripts, pipelines, and basic redirections.

## Features

- Built-ins: `cd`, `pwd`, `echo`, `env`, `setenv`, `unsetenv`, `which`, `alias`, `unalias`, `history`, `source` (or `.`), `jobs`, `fg`, `bg`, and `exit`.
- External commands launched through the system's `PATH`.
- Single and double quote handling in command arguments.
- Pipelines using `|`.
- Input redirection with `<`, output redirection with `>`, and append redirection with `>>`.
- Command sequencing and conditional operators: `;`, `&&`, and `||`.
- Background commands using `&`, with basic `jobs`, `fg`, and `bg` support.
- Command substitution using `$(...)`.
- Command history and aliases, saved in `.las_shell_history` and `.las_aliases` in the current working directory.
- Script execution from a file.
- A prompt that displays the current directory and last command status.

This is a learning project and does not aim to implement every behavior or edge case of Bash or POSIX shells.

## Requirements

- Linux or another Unix-like operating system.
- GCC and GNU Make.
- GNU Readline development headers and library.

On Debian or Ubuntu, install the build dependencies with:

```sh
sudo apt install build-essential libreadline-dev
```

## Build

```sh
git clone https://github.com/dhiaelhack/LAS_Shell_DSH.git
cd LAS_Shell_DSH
make
```

The build creates the `las_shell` executable in the project directory. To remove generated object files and the executable, run `make clean`.

## Run

Start an interactive session:

```sh
./las_shell
```

Run a script file:

```sh
./las_shell path/to/script.sh
```

Run one command and exit:

```sh
./las_shell -c 'echo hello'
```

## Examples

```sh
pwd
cd /tmp
echo "Current directory: $(pwd)"
ls -la | grep README
echo hello > greeting.txt
echo again >> greeting.txt
cat < greeting.txt
false || echo "The previous command failed"
sleep 10 &
jobs
alias ll='ls -la'
ll
```

Aliases can also be managed with `unalias name`. The `source file` command executes commands from a file in the current shell session. History and aliases are loaded and saved between sessions in the current working directory.

## Project layout

| File | Responsibility |
| --- | --- |
| `main.c` | Interactive shell loop, prompt input, and command dispatch |
| `Commands.c` | Built-in commands and script/source command handling |
| `input_parser.c` | Tokenization and quote handling |
| `pipes.c` | Pipeline parsing and execution |
| `redirection.c` | Input and output redirection |
| `operators.c` | Command sequencing and basic job tracking |
| `substitution.c` | `$(...)` command substitution |
| `script.c` | Script and command-line execution paths |
| `alias.c` | Alias storage, persistence, and expansion |
| `history.c` | Readline history, signal handling, and completion |
| `prompt.c` | Prompt generation and exit status |
| `helper.c` | String and environment helper functions |
| `my_own_shell.h` | Shared declarations and data structures |
| `makefile` | Build rules |

## Notes

- The implementation is intentionally compact and has not been verified as a complete POSIX shell. Complex quoting, nested combinations of operators, and advanced job control may behave differently from Bash.
- The makefile links against GNU Readline with `-lreadline`.
- `make clean` also removes `.las_shell_history` and `.las_aliases` from the project directory.
