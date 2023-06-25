# Process worksheet 4

1. Unix I/O isn't buffered, standard I/O is
2. A table with open files, containing mode, refcount, and inode
3. It's copied
4. Both file descriptor entries point to the same inode
5. How many times the file's been opened
6. It gets removed from the table
7. `close`
8. Redirect input or output from one file to another
9.

```c
void read_and_average() {
  int a, b, c;

  scanf("%d %d %d", &a, &b, &c);
  printf("%d\n", (a + b + c) / 3);
}

int main() {
  int fd = open("data.txt", O_RDONLY);
  dup2(fd, STDIN_FILENO);
  read_and_average();
}
```
