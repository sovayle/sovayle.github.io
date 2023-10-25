Reverse Engineering 101

> book : Practical Malware Analysis book by Sikorski & Honig

# low-level hanging fruit

XOR = ^
X ^ Y = Z
Y ^ Z = X

encoded += chr((ord(i)^5))
### strace
trace system calls

### ltrace 
library call tracer
runs the specified command until it exists
b
ltrace ./bbbbloat

objdump -d bbbbloat

find the main function

file bbbbloat (find stripped)

## GDB
useful for dynamic challenges
https://h0j3n.gitbook.io/ctf/reverse-engineering/introduction/tools

```
gdb-gef (run the tool)
gdb-gef ./simple_elf2

run
run 1234
b main 
disas main
b *0x00005555555551d2
c (continue)
print $eflags
```


windows dynamic analysis
x64/x86 dbg

strings - linux

dnspy -.net

androguard - mobile apk

apktool - mobile apk

```
file simple_elf1
./simple_elf1
strings simple_elf1 (cat simple_elf1 wont give good output because simple_elf1 is a binary file)
xxd simple_elf1 | grep H0j3nCTF (to show hex format)
strings simple_elf1 | grep H0j3nCTF
strace ./simple_elf2
ltrace ./simple_elf2 1111






```

## ida
Installation
```
download .deb file: https://hex-rays.com/ida-free/#download
chmod +x file.run
./file.run
echo 'export PATH=$PATH:/opt/file' >> ~/.bashrc
bash
ida64 (run prog in terminal)

(optional)
sudo ln -s /opt/idafree-8.3/ida64 /usr/local/bin/ida
ida (run prog in terminal from any working directory)
```

tools:
```
dnspy - decompile .NET exe to find Main function
olevba - analyze maldoc files (find sus echo strings that looks like base64)

executable and dll (learn what it is)

https://www.lddgo.net/en/string/pyc-compile-decompile - online python decompiler

```
forensics:

```
PECmd to read .pf files.

```

> RAX - Known as the accumulator register. Often used to store the return value of a function.

> RBX - Sometimes known as the base register, not to be confused with the base pointer. Sometimes used as a base pointer for memory access.

> RDX - Sometimes known as the data register.

> RCX - Sometimes known as the counter register. Used as a loop counter.

> RSI - Known as the source index. Used as the source pointer in string operations.

> RDI - Known as the destination index. Used as the destination pointer in string operations.

> RSP - The stack pointer. Holds the address of the top of the stack.

> RBP - The base pointer. Holds the address of the base (bottom) of the stack.








