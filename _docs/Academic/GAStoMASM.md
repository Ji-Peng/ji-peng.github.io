---
title: Convert GAS Syntax to MASM Syntax.
category: Cryptographic Engineering
order: 1
---
### 1.Introduction
My task is to convert GAS syntax to MASM syntax.

Finally, I realized converting under the help of a script(https://gist.github.com/Ji-Peng/439a4a863c085096f130c26cb75651d6).

### 2.Difference
I divide the distinction into two categories, syntax and calling convention.

For example:

#### 2.1.The difference of syntax
```c
GAS:
q_vector:
.double 12289.0
.double 12289.0
.double 12289.0
.double 12289.0

MASM:
q_vector real8 12289.0, 12289.0, 12289.0, 12289.0
```
---
```c
GAS:
.global ntt_double1024
ntt_double1024:

MASM:
public ntt_double1024
ntt_double1024 PROC
```
---
```c
GAS:
mov %rsp,%r11
and $31,%r11
add $0,%r11
sub %r11,%rsp

MASM:
mov r11,rsp
and r11,31
add r11,0
sub rsp,r11
push r11
```
---
```c
GAS:
vmovdqu q_vector(%rip),%ymm0

MASM:
vmovdqu ymm0,ymmword ptr[q_vector]
```
---
etc.
#### 2.2.The difference of calling convention
https://en.wikipedia.org/wiki/X86_calling_conventions

### 3.Tips
* Firstly, using my script mentioned above. 
* Then manually change the registers, because the calling convention of gas and masm is different.
* Unfortunately, my script is not perfect and it only handles a portion of the work.