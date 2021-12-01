---
title: 'Final Exam Notes'
date: 2007-05-22T19:00:00.000-07:00
draft: false
---

Syntactical error possibilities:  
operands consistent with operation? (e.g., byte/long)  
parameters allocated correctly? (order)  
local variables allocated correctly?  
storage space allocated on the stack for local vars?  
loops have unconditional jumps back to beginning?  
operands correct? (e.g., memory to memory)  
local/parameter memory access consistency  
jumping to correct labels? (e.g., begin while, not repeating init while)  
pointer operations correct? (e.g., gets pointer address, not pointer value)  
operands for add/sub/cmp correct? (e.g., addl %eax,$5)  
void \* dereference without cast?  
  
Strategies:  
comment code  
read ahead and find out use of registers  
no assembler-catchable errors  
  
  
Exit code:  
  
movl $1,%eax  
movl $0,%ebx  
int $0x80  
  
Function entrance code:  
//functionFoo(int \*paramOne, char \*paramTwo);  
oldEbp = 0  
retAddr = oldEbp + 4  
paramOne = retAddr + 4  
paramTwo = paramOne + 4  
localOne = oldEbp - 4  
localTwo = localOne - 4  
  
pushl %ebp  
movl %esp, %ebp  
  
addl $localTwo,%esp  
  
pushl %ebx  
pushl %ecx  
pushl %edx  
  
... function body ...  
  
popl %edx  
popl %ecx  
popl %ebx  
  
subl $localTwo,%esp  
  
popl %ebp  
  
ret  
  
Function call:  
// functionFoo(int \*paramOne, char \*paramTwo);  
  
pushl paramTwo(%ebp) // if paramTwo is char \*  
pushl paramOne(%ebp)  
call functionFoo  
addl $8,%esp  
  
  
Moving data:  
// if X\_size defined statically  
X\_size: .fill 4, 1, 0xff // X\_size is a memory address  
...  
movl X\_size,%eax // eax is 0xffffffff (go to the address and get the value)  
movl $X\_size,%eax // eax is 0x804909c (treat the address as a literal)  
// if X\_size defined as a value  
X\_size = 4 // X\_size is a value  
...  
movl X\_size,%eax // eax is 0x8049090 (go to the value's addr and get data)  
movl X\_size+3,%eax  
movl $X\_size,%eax // eax is 4 (treat the value as a literal)  
  
Incrementing pointers:  
  
q = p + 1 // q is int32 \*q; p is int32 \*p  
movl p(%ebp),%eax  
addl $4,%eax //4 because sizeof(int32) = 4  
  
Popping an element into memory:  
popl Y\_f1+X\_f1(%eax)  
  
Comparing byte:  
cmpb $'\\n',a+X\_ch(%ebp)  
  
$L1-2 evaluates L1-2 first