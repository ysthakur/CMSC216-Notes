# Review for quiz 2

1. 100011
2. 35
3. 3.5 = 2 + 1 + 0.5 = 2^1 + 2^0 + 2^(-1) = 2^1 * (1 + 0.5 + 0.25)
4. `2^(65 - 127) * (1.0101_2) = 2^(-62) * (1 + 1/4 + 1/16) = 2.84e-19`
5. V1 garbage
   V2 address
   V3 2
   Yes
6.

```c
FILE *file = fopen("data.txt", "r");
char buf[6];
fgets(buf, 6, file);
```

7. hi
   2
   8
9.

```c
typedef struct radio {
  int *years_on_air;
  char letter;
} Radio;

int main() {
  Radio *r;
  int age = 34;
  r->letter = 'A';
  r->years_on_air = &age;
  *(r->years_on_air) += 10;
}
```
