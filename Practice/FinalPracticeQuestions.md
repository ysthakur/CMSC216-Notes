# Finals Practice Questions

## Problem 1: Short answers

a. Statically linked is faster because the library is included with the executable.
   Dynamically linked: multiple libraries can share it. Slower to start up.
b. 32-bit floats have 1 sign bit, 8 exponent bits, and 23 significand bits
   The float is `sign bit * 2^(exponent - 127) * 1.significand`
c. Base conversion
  i. 41
  ii. 10011010
  iii. 11011011 -> 00100100 + 1 -> 00100101 -> -37
  iv. `16 * 10 + 11 = 171`
  v. 1010 1011 1100 1101
  vi. `174 = 16 * 10 + 14 = AE_16`
d. `<` makes it take input from the given file, `>` redirects output to the given file
e. `int* const a` means that the variable `a` cannot be modified, but the `int` that
   it's pointing to can. `const int *a` means that the variable `a` can be modified
   inside the function, but the `int` it's pointing to cannot be.
f. For threads: `pthread_join(tid, &ret);` for threads, `wait_pid(child_pid, &status, 0);` for processes

## Problem 2

```text
2 and 7
Jones
e and e
f and s
3 and 4
```

## Problem 3

```text
5 11 0
11 7 11
??? ??? 11
```

## Problem 4

```c
void my_system(char *string) {
  int child_pid = fork();

  if (child_pid == -1) {
    perror("fork");
    exit(-1);
  } else if (child_pid) {
    if (wait(NULL) == -1) {
      perror("wait failed");
      exit(-1);
    }
  } else {
    char *argv[41];
    parse(string, argv);
    execvp(argv[0], argv);
    perror("Failed to execute");
    exit(-1);
  }
}
```

## Problem 5

```c
static pthread_mutex_t mutex;

void init() {
  pthread_mutex_init(&mutex, NULL);
}

int deposit(Account *account, unsigned int amount) {
  int new_balance;
  pthread_mutex_lock(mutex);
  account->balance += amount;
  new_balance = account->balance;
  pthread_mutex_unlock(mutex);
  return new_balance;
}

int withdraw(Account *account, unsigned int amount) {
  int new_balance;
  pthread_mutex_lock(mutex);
  account->balance -= amount;
  new_balance = account->balance;
  pthread_mutex_unlock(mutex);
  return new_balance;
}
```
