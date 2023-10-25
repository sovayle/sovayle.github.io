---
title: "UTAR The Amazing Cyberhunt"
#categories: 
permalink: /ctfs/utar-the-amazing-cyberhunt
---

> CTF UTAR

# Introduction

This is writeup for UTAR CTF

![certificate](/assets/c/The_Amazing_Cyberhunt_AmirulAzim.jpg)

# Physical challenge

## Hash

**A Hash is Given: df8287309c06b3395f14145fd49fc4088d1236425c71f13a0efc38602de23f90**

Using [hashes.com](https://hashes.com/en/decrypt/hash), the decryption will give us:

**df8287309c06b3395f14145fd49fc4088d1236425c71f13a0efc38602de23f90:16052**

which at the end is **16052**.

Go to UTAR Staff directory website.

Each staff ID will have 4 numbers. If clicked on a staff, the URL at the end will have 5 digits for example:
"searchId=12345". Replace the 5 digits with '16052' and a Staff name will be given. Find the staff to receive a pendrive.

## .pdf 
When opening the .pdf file, an error shows. When checking the file extension using hex editor tool like HxD, we can see that the extension is for .wav and when changing extensions, playing the wav file will play UTAR song.

using [morsecodeworld's audio decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) we see in the middle of the song that a morse code can be heard, and morse code world will output the flag in the frequency translator section.

# Online challenge

Coming soon...







