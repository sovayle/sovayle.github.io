---
layout: single
title: "TryHackMe"
permalink: /ctfs/tryhackme
toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
---

> TryHackMe Writeups

# Introduction

This is writeup for TryHackMe challenges

## RE

### BasicMalwareRE

install 7zip:

#### Task3

unzip:

7za e strings2.zip

using chatgpt, convert the HEX values into ASCII.
```
local_2c = 'F'
local_2b = 'L'
local_2a = 'A'
local_29 = 'G'
local_28 = '{'
local_27 = 'S'
local_26 = 'T'
local_25 = 'A'
local_24 = 'C'
local_23 = 'K'
local_22 = '-'
local_21 = 'S'
local_20 = 'T'
local_1f = 'R'
local_1e = 'I'
local_1d = 'N'
local_1c = 'G'
local_1b = 'S'
local_1a = '-'
local_19 = 'A'
local_18 = 'R'
local_17 = 'E'
local_16 = '-'
local_15 = 'B'
local_14 = 'E'
local_13 = 'S'
local_12 = 'T'
local_11 = '-'
local_10 = 'S'
local_f = 'T'
local_e = 'R'
local_d = 'I'
local_c = 'N'
local_b = 'G'
local_a = 'S'
local_9 = '}'
```

Presenting them in a row will get us the flag.

flag: FLAG{STACK-STRINGS-ARE-BEST-STRINGS}


#### Task4

look at 'entry' function in GHidra, a variable called FindResourceA and LoadStringA has a comment in Assembly "FLAG{RESOURCES-ARE-POPULAR..}

by going to Ghidra > Search> For Strings... we type in the string and it will lead us to the flag.

OR

loadStringA has a parameter '0x110' and in decimal, it is 272. According to the list of Strings in assembly, all of them have a Rsrc String ID starting from 0..and the flag is the ID 272.

flag: FLAG{RESOURCES-ARE-POPULAR-FOR-MALWARE}



### Reversing ELF

#### Task1 : Run the file

Flag: flag{not_that_kind_of_elf}


#### Task2: 

What is the super secret password ?

solution: use ghidra and check the parameters for any strings.

OR

ltrace ./crackme2 1234

super_secret_password

Flag: flag{if_i_submit_this_flag_then_i_will_get_points}


#### Task3: 

Found clue on function "FUN_080484f4" a string compare.
flag in base64:

ZjByX3kwdXJfNWVjMG5kX2xlNTVvbl91bmJhc2U2NF80bGxfN2gzXzdoMW5nNQ==

decoded will get the flag.

Flag: f0r_y0ur_5ec0nd_le55on_unbase64_4ll_7h3_7h1ng5

#### Task4:

ltrace:

```
┌──(root㉿kali)-[/home/kali/Downloads/TryHackMe/ReversingELF]
└─# ltrace ./crackme4 tes
__libc_start_main(0x400716, 2, 0x7ffcde2f24e8, 0x400760 <unfinished ...>
strcmp("my_m0r3_secur3_pwd", "tes")            = -7
printf("password "%s" not OK\n", "tes"password "tes" not OK
)        = 22
+++ exited (status 0) +++
```

gdb-gef: 

```
gef➤ info functions
gef➤ b *0x0000000000400520
gef➤  info b
gef➤  delete 1
gef➤ b *0x0000000000400520
gef➤ run test
gef➤  info registers (general purpose registers rax and rdx have memory address values)
gef➤  x/s 0x7fffffffe130
0x7fffffffe130: "my_m0r3_secur3_pwd"
```

frida:

frida -l hook.js ./crackme4 asd

#### Task5

```
┌──(root㉿kali)-[/home/kali/Downloads/TryHackMe/ReversingELF]
└─# ltrace ./crackme5
strncmp("1", "OfdlDSA|3tXb32~X3tX@sX`4tXtz", 28) = -30

┌──(root㉿kali)-[/home/kali/Downloads/TryHackMe/ReversingELF]
└─# ./crackme5       
Enter your input:
OfdlDSA|3tXb32~X3tX@sX`4tXtz
Good game
```
gdb-gef:
memory address string values for the rax and rcx registers gives the necessary input to get the output message “Good game”.

```
gef➤  x/s 0x7fffffffe120
0x7fffffffe120: "cow"
gef➤  x/s 0x7fffffffe140
0x7fffffffe140: "OfdlDSA|3tXb32~X3tX@sX`4tXtz"
```

flag: OfdlDSA|3tXb32~X3tX@sX`4tXtz

#### Task6

solution: read the source codes

undefined8 my_secure_test(char *param_1)

```
  if ((*param_1 == '\0') || (*param_1 != '1')) {
    uVar1 = 0xffffffff;
  }
  else if ((param_1[1] == '\0') || (param_1[1] != '3')) {
    uVar1 = 0xffffffff;
  }
  else if ((param_1[2] == '\0') || (param_1[2] != '3')) {
    uVar1 = 0xffffffff;
  }
  else if ((param_1[3] == '\0') || (param_1[3] != '7')) {
    uVar1 = 0xffffffff;
  }
  else if ((param_1[4] == '\0') || (param_1[4] != '_')) {
    uVar1 = 0xffffffff;
  }
  else if ((param_1[5] == '\0') || (param_1[5] != 'p')) {
    uVar1 = 0xffffffff;
  }
  else if ((param_1[6] == '\0') || (param_1[6] != 'w')) {
    uVar1 = 0xffffffff;
  }
  else if ((param_1[7] == '\0') || (param_1[7] != 'd')) {
    uVar1 = 0xffffffff;
  }
```

flag: 1337_pwd

#### Task7

solution: run ghidra and see the main function, local 14 needs to be equal to 0x7a69, converting this hex to dec, we will get 31337.. entering this number when we run the program with ./crackme7 will give us the flag

flag: flag{much_reversing_very_ida_wow}


#### Task8

solution: run ghidra and see the main function, iVar2 needs to be equal to -0x35010ff3, converting this hex to dec, we will get -889262067.. entering this number when we run the program with ./crackme8 will give us the flag

```┌──(root㉿kali)-[/home/kali/Downloads/TryHackMe/ReversingELF]
└─# ./crackme8 -889262067
Access granted.
flag{at_least_this_cafe_wont_leak_your_credit_card_numbers}
```

### REloaded

#### Task1

solution:

strings: strings Level.exe | grep -E '.{10,100}'

this filters the flag length from 10 to 100 characters

we can see 'L3v3lZ340_is_D02e' as one of the strings

OR 

Ghidra strings

#### Task 2

solution: run ghidra, look at strings.. "Thats your lucky number !!!" seems like tha flag. Double click it to see the location in the assembly, highlight the string > right click > Show References to "Thats your lucky number !!!". This will take us to a function, and we can see in param1 there is a hex "0x6ad" in the decompiler, this hex converted to decimal gives us 1709. And running wine Level.exe 1709, the program will tell us that it is the lucky number.


Flag: 1709

#### Task 3

solution: similarly to task 2, we find the string. In this case it is "Get Ready For L4 ;)". We can see in function 'FUN_00401410' line 17, that iVar1 uses comparison of local20 and param 1. Highlight line 18 and we can see a JNZ instruction. Let's patch the assembly by changing the JNZ to JZ. Highlight JNZ > right click > Patch Instruction. Now we have to save the file. we can use a python script to save the file. We add a new file at Window > Script Manager. Here, add a new script from [savePatch](https://github.com/schlafwandler/ghidra_SavePatch) and use savepatch to save a new .exe file. Lastly, run the exe file and we succesfully get our flag with any input.

flag: L3_1s_20t_Th3_L131t

Which instruction did you modified?: jnz

#### Task 4

solution: We first run the exe file and see a clue of string called "Rooted".By trailing Rooted in Ghidra, we can see that it leads to function 'FUN_00401410'. By highlighting the function in source code, we find memory address 004014bc. We can use Immunity Debugger to reveal the real password when the program is excuting in memory.

open Level.exe in Immunity Debugger and set a breakpoint (F2) at the memory address 004014bc. Then, run (F9) the program and enter a wrong password and press F7 to continue to the next memory address. We continue until we see the flag in the registers.

flag: THMctf-L4

#### Task 5

the program closes itself if we run it. So we load the binary into Ghidra to see anything we can use. No strings can be seen, but the program did print something on the screen when we ran it. This could be a print statement. so we search for any printf functions in the assembly under Search > Program Text. 


we can see the one of the printf statements has a reference 'FUN_00401453:004014da(c)' and clicking on it will lead us to 004014da memory address. The primary function 'Fun_00401453' might have clues so we highlight it and check for references. This will lead us to memory address 00401532. we will try to find the flag by launching Immunity Debugger and setting a breakpoint(F2) here and continuing the program with (F7) and we will get the flag.

flag: Alan Turing Was a Geniuse





