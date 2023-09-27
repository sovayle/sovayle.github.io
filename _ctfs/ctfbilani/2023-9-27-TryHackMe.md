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

Task1 : Run the file

Flag: flag{not_that_kind_of_elf}


Task2: 

What is the super secret password ?

solution: use ghidra and check the parameters for any strings.

super_secret_password

Flag: flag{if_i_submit_this_flag_then_i_will_get_points}















