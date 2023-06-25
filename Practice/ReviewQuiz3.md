# Homework 10 spring 2022

1.

```asm
#prologue
subu $sp, $sp, 8
sw   $ra, 8($sp)
sw   $fp, 4($fp)
addu $fp, $sp, 8

la   $t0, x
lw   $t1, ($t0)
add  $t1, $t1, 1
sw   $t1, ($t0)

#epilogue
move $sp, $fp
lw $ra, ($sp)
lw $fp, -4($sp)
jr ra
```

2.

```asm
#prologue

subu $sp, $sp, 12    # grow stack for local vars

add  $t0, $sp, 12
add  $t1, $sp, 8
add  $t2, $sp, 4
subu $sp, $sp, 12    # grow stack for args
sw   $t0, 12($sp)
sw   $t1, 8($sp)
sw   $t2, 4($sp)
jal scanf

lw $t0, 12($sp)      # load a
lw $t1, 8($sp)       # load b
lw $t2, 4($sp)       # load c

mul $t2, $t1, $t2    # t2 <- b*c
add $t2, $t0, $t2    # t2 <- a+t2

move $a0, $t2
li $v0, 1
syscall              # print new c

#epilogue
```

3.

```asm
add $t0, $a0, $a1
div $t0, $a2, $t0

move $a0, $t0
li $v0, 1
syscall
```

4.

```assembly
subu $sp, $sp, 4
...?
```

5.

```asm
#prologue

li $a0, 123
li $a1, 456
jal i

li $v0, 0

#epilogue
```

6.

```asm
li $v0, 789
```

7.

```
jal k

move $a0, $v0
li $v0, 1
syscall
```

8.

```

```

9.

```
la $t0, a
li $t1, 3
sw $t1, ($t0)

la $t0, b
li $t1, 5
sw $t1, ($t0)

move $a0, $t0
move $a1, $t1
jal l

la $t0, c
lw $v0, ($t0)
```
