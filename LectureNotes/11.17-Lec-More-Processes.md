# More processes

## Variables

- Environment variable examples:
  - `PATH`: where the shell looks for programs
  - `PAGER`: what program to use to view files one page at a time (e.g. `less`)
- Shell/local variables only affect current shell, while environment variables
  are copied to all child processes run by shell
- Setting shell variables:
  - tcsh: `set var=value`
  - bash: `var=value`
- Can change prompt with `set prompt=...`
- Setting environment variables:
  - tcsh: `setenv VAR value`
  - bash: `export VAR=value`

### Environment variables

- In C program, can access environment variables with 3-argument main:
  - `envp` is an array of strings of the form `NAME=VALUE` with the last one being `NULL`

```c
int main(int argc, char *argv[], char *envp[]) {...}
```

- The `extern char **environ` (declared in `unistd.h`) also holds the current environment
  in the same form as `envp`
- Can get the value associated with an environment variable using `char *getenv(const char *name)`
  - Requires `stdlib.h`
- Can get working directory of a program using `char *getcwd(char *path, size_t size)`
  - Requires `unistd.h`
  - `path` is where to output
  - `size` is size of your
- Can change working directory using `int chdir(const char *path)`
  - Requires `unistd.h`
  - Returns -1 on error

## Loading a new program

- The `exec*` family of system calls can be used to load a program in the context of the current process
- It's the same process, but running a different program
  - Essentially replaces the current program with another while it's running
- The code, static data, stack, and heap are all replaced
- The process is the same (same pid, same parent)
- `exec*` system calls return -1 on error, they don't return at all on success

### `execl`

```c
int execl(const char *filename, const char *arg0, ..., NULL);
```

- Arguments are
  - `filename`: program name
  - Then the alias, usually same as program name
  - Then the actual arguments for the program
  - `NULL` to mark end of arguments
- Example: `execl("/bin/ls", "ls", "-l", NULL);`
- Can execute programs we made, not just Unix commands

### `exec*` function naming

Each `exec*` function has the name `exec` followed by a combination of `l`, `v`, `p`, `e`

- `l`: Use an argument **l**ist, terminated by `NULL`
- `v`: Use an argument array (**v**ector) (instead of a **l**ist)
- `p`: Search the **P**ATH list of directories to find the program to execute (otherwise, need absolute path)
- `e`: Use the specified **e**nvironment

If the prototype has an argument called `filename`, you need to specify the absolute path of the executable

## `waitpid` system call

- Supersedes `wait`
- Waits on one specific process
- Can specify the ID of the child we're waiting for
- Can specify other options through the `options` parameter
  - `options` is a number formed using bitwise OR of several flags (or 0)
  - `WNOHANG` is the most useful of these flags (doesn't block parent if no child)

## Background processing

- Shells can do background processing (e.g. `a.out &`) to run next command without waiting
  for current command to finish

- Shell needs to reap using `waitpid` every so often to make sure zombies are taken care of
