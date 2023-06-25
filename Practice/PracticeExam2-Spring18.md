# Practice exam 2, Spring 2018

## Problem 1

1. `double *(*task)(int * float);`
2. `tar xf my_examples.tar.gz`
3. c
4. b
5.

```c
table.o: table.c table.h bucket.h
<tab>gcc -g -c table.c
```
6. 2
7. `grep TODO *.c`
8.

```c
unsigned char flip_nibbles(unsigned char val) {
  return ((val >> 12) & 0x000F) | ((val >> 4) & 0x00F0) | ((val << 4) & 0x0F00) | ((val << 12) & 0xF000);
}
```

9.

```c
return *((char *) &value) == 0x67;
```
