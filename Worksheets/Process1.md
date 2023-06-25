# Process worksheet 1

1. The kernel manages files, processes, and a bunch of other stuff
2. syscalls, ???
3. A process can have multiple threads that share memory. Two processes don't share memory.
4. A processor runs one process, suspends it, runs another, then maybe comes back
5. init
6. SIGSEGV, SIGKILL
7. Too many processes
8. 3
9.

```c
void process(int parent_value, int child_value) {
  if (fork()) {
    printf("Parent value: %d\n", parent_value * parent_value);
  } else {
    printf("Child value: %d\n", child_value * child_value);
    exit(0);
  }
}
```
