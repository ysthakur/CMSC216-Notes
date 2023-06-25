# Practice for final (from CMSC_216_PRACTICE_SET.pdf)

## Basic Linux Commands

1. `mkdir Professors`
2. `mkdir -p Professors/Yoon Professors/Herve && cd Professors/Yoon`
3. `touch grades.txt`
4. `cd ~`
5. `ls Professors`
6. `cp Professors/Yoon/grades.txt Professors/Herve`

## Input Output Redirection

```bash
./a.out < public01.in > public01.output
```

## Functions

1. "6"
2. Doesn't compile - **Wrong** - does compile and prints garbage
3. Garbage

## Compilation

1. Translation
2. Dereferencing a null pointer (e.g. `*NULL`)
3. `int x; printf("%d", &x);`

## Makefile

```make
human.o: human.c head.h body.h feet.h
  $(CC) $(CFLAGS) -c human.c
```

## Structs

Size of struct is 4 + 4 + 5 = 13, but for alignment, becomes 16

## Memory

1. `malloc` takes only the number of bytes to allocate memory for and returns a pointer
   to the allocated memory without initializing it, while `calloc` takes the number of
   elements and the size of each element and also initializes to 0.
2. Yes.
3. If it was allocated on the heap, the memory becomes part of pool of free memory
4. Yes, if you free something that isn't dynamically allocated or was already freed.

## Process

1. Gives you the child's exit status or the signal that killed it, whichever is applicable
2. `WIFEXITED` tells you if the child exited normally. Then you can use `WEXITSTATUS` to
   determine the exit code it exited with.
3. `$PATH`, `$HOME`. Local variables only available in current shell, environment
   variables available even in programs you run from current shell
4. Just "Hello\n" and whatever the command prints
5. It needs to have a `NULL` at the end of `argv`
6.

```c
int main() {
  if (fork() == 0) {
    char *argv[] = {"print_triangle", NULL};
    execvp(argv[0], argv);
  } else {
    int status;
    wait(&status);
    if (WIFEXITED(status)) printf("%d", WEXITSTATUS(status));
  }
}
```

7. `int fd = open("message.txt", O_RDONLY);`
8. True/False
  1. False? Processes have file descriptor tables
  2. False, files can be opened multiple times
  3. False, other processes would still have that file open
9. Permissions, environment, signal handling settings, current working directory, root directory, resource limits, controlling terminal, a copy of the stack, register, heap, file descriptor table.
10. Child adopted by init, reaped when it terminates
11. **todo** see lecture slides for visualization of file descriptors and stuff
    Each process has a file descriptor table stored in the kernel.
    The open file table is also in the kernel.
12. When redirecting input or output from one file to another
13. You won't be able to detect that it's ended
14. **todo** look up the difference between pipes and redirection
    I/O redirection makes one file descriptor point to another file, while a pipe can be used for
    communicating between processes.
15. **todo** look up what happens to file descriptors after a dup2 call
16. A process can have multiple threads. Threads have their own stack and register but share the heap and everything else.
17. **todo** look up what the address space is
