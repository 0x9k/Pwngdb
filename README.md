# Pwngdb

GDB for pwn.

## Install

### install
	cd ~/
	git clone https://github.com/0x9k/Pwngdb.git 
	cp ~/Pwngdb/.gdbinit ~/

If you dont want to use gdb-peda , you can modify the gdbinit to remove it.

### Heapinfo 

If you want to use the feature of heapinfo and tracemalloc , you need to modify some val of pwngdb.py

+ heapinfo
	+ `main_arena_off` : The offset of `main_arena` in glibc
	+ `main_arena_off_32` : The offset of `main_arena` in glibc32
+ tracemalloc
	+ `main_arena_off` : The offset of `main_arena` in glibc
	+ `main_arena_off_32` : The offset of `main_arena` in glibc32
	+ `_int_malloc_off` : The offset of `_int_malloc_off` in glibc
	+ `_int_malloc_off_32` ; The offset of `_int_malloc_off` in glibc32
	+ `_int_free_off` : The offset of `_int_free_off` in glibc
	+ `_int_free_off_32` :The offset of `_int_free_off` in glibc32
	+ `malloc_off` : The offset of `malloc` in glibc
	+ `free_off` : The offset of `free` in glibc

## Features

+ `libc` : Print the base address of libc
+ `ld` : Print the base address of ld
+ `codebase` : Print the base of code segment
+ `heap` : Print the base of heap
+ `got` : Print the Global Offset Table infomation
+ `dyn` : Print the Dynamic section infomation
+ `findcall` : Find some function call 
+ `bcall` : Set the breakpoint at some function call
+ `tls` : Print the thread local storage address
+ `at` : Attach by process name
+ `findsyscall` : Find the syscall
+ `fmtarg` : Calculate the index of format string
	+ You need to stop on printf which has vulnerability.
+ `force` : Calculate the nb in the house of force.
+ `heapinfo` : Print some infomation of heap
+ `chunkinfo`: Print the infomation of chunk
    + chunkinfo (Address of victim)
+ `chunkptr` : Print the infomation of chunk 
	+ chunkptr (Address of user ptr)
+ `mergeinfo` : Print the infomation of merge
	+ mergeinfo (Address of victim)
+ `printfastbin` : Print some infomation of fastbin
+ `tracemalloc on` : Trace the malloc and free and detect some error .
	+ You need to run the process first than `tracemalloc on`, it will record all of the malloc and free.
	+ You can set the `DEBUG` in pwngdb.py , than it will print all of the malloc and free infomation such as the screeshot.
+ `parseheap` : Parse heap layout


## Debug PIE
+ `set_breakpoint_pie` : set breakpoint with pie program

```python

#python exp debug template

from pwn import *

r = process("./xxxx")

def attach():
    gdb.attach(r, execute='''
        set_breakpoint_pie 0xda5
        c
            ''')
    raw_input("joker")
    #echo 0 | sudo tee /proc/sys/kernel/yama/ptrace_scope
    #0xda5 offset address in program
    
....

attach()#automatic to set breakpoint
...

r.interactive()

```


## Screenshot

+ Chunkinfo

![chunkinfo](http://i.imgur.com/gtQuIsL.png)
+ Mergeinfo

![chunkinfo](http://i.imgur.com/TjWkzGc.png)
+ Heapinfo

![heapinfo](http://i.imgur.com/xhTc8Gv.png)

+ tracemalloc

![trace](http://i.imgur.com/7UHqiwX.png)
