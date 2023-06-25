# Process worksheet 3

1. Its memory is reclaimed by the kernel, it's removed from the list of running processes
2. The first child process to end
3. Returns -1
4. `WIFEXITED(status) && WEXITSTATUS(status) == SIGSEGV`
5. No
6. It will be replaced
7. Executable not found
8. `waitpid(-1, &status, 0)`
9.

```c
char month[5];
scanf("%s\n", month);
if (fork()) {
  if (!fork()) {
    execlp("cal", "cal", month, NULL);
  }
  wait(NULL);
  wait(NULL);
} else {
  execlp("date", "date", NULL);
}
```
