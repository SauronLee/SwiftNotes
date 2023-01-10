アセンブリ言語 (Assembly Language)
=================================


Register
------------



+---------------------+-------------------------+---------------------------------+------------------------------------------------------+
|  Item               | AT&T                    | Intel                           | Subscript                                            |
+=====================+=========================+=================================+======================================================+
| Register naming     | %rax                    | rax                             |                                                      |
+---------------------+-------------------------+---------------------------------+------------------------------------------------------+
| Assignment          | movq %rax, %rdx         | mov rdx, rax                    | rax -> rdx                                           |
+---------------------+-------------------------+---------------------------------+------------------------------------------------------+
| Constant assignment | movq $0x10, %rax        | movq rax, 0x10                  | 0x10 -> rax                                          |
+---------------------+-------------------------+---------------------------------+------------------------------------------------------+
| Memory assignment   | movq $0xa, 0x1ff7(%rip) | mov qword ptr [rip+0x1ff7], 0xa | 0xa -> rip+0x1ff7(address)                           |
+---------------------+-------------------------+---------------------------------+------------------------------------------------------+
| Address assignment  | leaq -0x18(%rbp), %rax  | lea rax, [rbp-0x18]             | rbp-0x18(address) -> rax                             |
+---------------------+-------------------------+---------------------------------+------------------------------------------------------+
| Jump                | jump *%rdx              | jump rdx                        |                                                      |
+---------------------+-------------------------+---------------------------------+------------------------------------------------------+
|                     |                         |                                 |  * b = byte(8-bit)                                   |
|                     |                         |                                 |  * s = short(16-bit integer or 32-bit floating point)|
|                     |                         |                                 |  * w = word(16-bit)                                  |
|   Size type         |   movel %eax, %edx      |     movel eax, edx              |  * l = long(32-bit integer or 16-bit floating point) |
|                     |                         |                                 |  * q = quad(64-bit)                                  |
|                     |                         |                                 |  * t = ten bytes(80-bit floating point)              |
+---------------------+-------------------------+---------------------------------+------------------------------------------------------+




| %rax, %rcx, %rdx, %rsi, %rdi, %rbp, %rsp  
| %r8, %r9, %r10, %r11, %r12, %r13, %r14, %r15

* %rax: the return of the function
* %rsi, %rdi, %rcx, %rdx, %r8, %r9: parameters of the function
* %rsp, %rbp: stack


Read the value of the register

* ``register read/numFormat``
  
  * numFormat: Hexades(x), floating points(f), decimal(d)
  
* ``register read/x``

Modify the value of a register

* ``register write register_name register_value``
* ``register write rax 0``

Displays the current values of all register  

* ``register read``
  
Show the value of the register  

* ``x/numFormat, Byte_size Memory_address``
  
  * numFormat: Hexades(x), floating points(f), decimal(d)
  * Byte_size: byte(b), helf word(h), word(w), giant word(g)

Modify the value in memory

* ``memory write Memory_address value``

Debugging

* ``thread step-over`` == ``next`` == ``n``
* ``thread step-in`` == ``step`` == ``s``
* ``thread step-inst-over`` == ``nexti`` == ``ni``
* ``thread step-inst`` == ``stepi`` == ``si``
* ``thread step-out`` == ``finish``








