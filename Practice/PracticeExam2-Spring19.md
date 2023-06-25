# Exam 2, Spring 2019

## Problem 1

1. `grep DEC *.h`
2. `chmod 511 exp`
3. d
4. c
5. `typedef double Values[2];`
6. Uses `sizeof` instead of `strlen`. `sizeof(p)` will just be the size of a pointer, which very likely won't be big enough.
7. `double (*fp)(int *, char);`
8. `01111`
9. 34, 12, cd, ab
10. 3
11. k (addr) -> t (trash)
12. `b = calloc(10, sizeof(Banana *));`
13. x: 0101 0111
    y: 0100 1011
    |: 0101 1111 = 4f
    ^: 0001 1100 = 1c
    Output:
    V1 4f
    V2 1c
14. Makefile:

```c
pt: pt.c seg.h
<tab>gcc -o pt pt.c
```

15. Function:

```c
uint16_t flip_clear_nibbles(uint16_t x) {
  return (x >> 4 << 12 >> 4) | (x << 4 >> 12 << 4);
}
```

## Problem 2

```c
int process_items(FILE *in, FILE *out) {
  int total_items;

  while (!feof(in)) {
    double version;
    char cable_type[20];
    int num_cables;

    if (fscanf(in, "software %f\n", &version) == 1) {
      fprintf(out, "software version %f requested\n", version);
      total_items ++;
    } else if (fscanf(in, "cables %s %d", cable_type, &num_cables) == 2) {
      fprintf(out, "%d cable(s) type %s requested\n", num_cables, cable_type);
      total_items ++;
    } else {
      char c;
      fprintf(out, "Invalid request\n");
      while (fgetc(in, &c) != NULL && c != '\n');
    }
  }

  fclose(out);
}
```

## Problem 3

1. create_list

```c
void create_list(const char *name, const Show *show, List **list) {
  if ((*list = malloc(sizeof(List))) == NULL) {
    return;
  }

  (*list)->size = 1;

  if (((*list)->name = malloc(strlen(name) + 1)) == NULL) {
    return;
  }

  strcpy((*list)->name, name);

  if (((*list)->head = calloc(1, sizeof(Node))) == NULL) {
    return;
  }

  if (((*list)->head->show = malloc(sizeof(Show))) == NULL) {
    return;
  }

  *(*list)->head->show = *show;
}
```

2. find_shows

```c
int find_shows(List *list, int channel, char result[][MAX_LEN + 1]) {
  int i = 0;
  Node *curr;

  if (list == NULL || result == NULL || channel < 1) {
    return -1;
  }

  curr = list->head;

  while (curr) {
    if (curr->show->channel == channel) {
      strcpy(result[i], curr->show->name);
      i ++;
    }

    curr = curr->next;
  }

  strcpy(result[i], "");

  return 0;
}
```

3. remove_first_show

```c
void remove_first_show(List **list) {
  Node *head = (*list)->head;
  (*list)->head = head->next;
  (*list)->size --;
  free(head->show);
  free(head);
  if ((*list)->size == 0) {
    free((*list)->name);
    free(*list);
    *list = NULL;
  }
}
```
