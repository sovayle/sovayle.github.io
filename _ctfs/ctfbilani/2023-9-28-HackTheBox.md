---
layout: single
title: "HackTheBox"
permalink: /ctfs/hackthebox
toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
---

> HackTheBox Writeups

# Introduction

This is writeup for Hack The Box challenges

# RE

### Behind The Scenes

solution:

Looking at the main function, we can see invalidInstructionException function,
by inspecting it, it points to memory addres 001012e6 with the instruction 'UD2' and there Ghidra has not assembled the instructions below UD2.. Assemble the code by highlighting all unassembled code and press 'D', and replace all UD2 instruction with 'NOP', the source code will now show nested if statements that reveal the flag.




%s

```
iVar1 = strncmp(*(char **)(in_RSI + 8),"Itz",3)
if (iVar1 == 0) 
iVar1 = strncmp((char *)(*(long *)(in_RSI + 8) + 3),"_0n",3)
if (iVar1 == 0) 
iVar1 = strncmp((char *)(*(long *)(in_RSI + 8) + 6),"Ly_",3)
if (iVar1 == 0) 
iVar1 = strncmp((char *)(*(long *)(in_RSI + 8) + 9),"UD2",3)
if (iVar1 == 0) 
printf("> HTB{s}\n",*(undefined8 *)(in_RSI + 8))
uVar2 = 0
```

Alternatively, we can run hexeditor on linux and type 'ctrl+w' to search for the flag. The keyword being 'HTB'

flag: HTB{Itz_0nLy_UD2}