---
title: "Sysinternals"
categories: knowledge
permalink: /blogs/sysinternals
toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
---

# Sysinternals

50+ windows tools

- File and Disk Utilities
- Networking Utilities
- Process Utilities
- Security Utilities
- System Information
- Miscellaneous

# File and disk utilities

## Sigcheck

- shows file version number, timestamp, digital signature, certificate chain and check file status on VT

sigcheck -u -e C:\Windows\System32

^ check for unsigned files in sys32

-u for VT check

-e is to scan executable images only

## Streams

- Alternate Data Streams ADS
- used to check $DATA of files

streams -accepteula

streams pathToFile —accepteula

streams "C:\Users\Administrator\Desktop\file.txt" -accepteula

notepad file.txt:ads.txt

## SDelete

- Allows to delete 1 or more file/directories

# Networking Utilities

## TCPiew

- show detailed listings of all TCP and UDP endpoints
- can use Resource Monitor windows built in utility too

tcpview -acepteula

# Process utilities

## Autoruns

- shows what programs are configured to run during system bootup or login
- good tool to search for any malicious entries created in the local machine to establish persistence

autoruns

## ProcDump

- command line utility whose primary purpose is monitoring an application for CPU spikes and generating crash dumps during a spike that an admin or dev can use to determine casue of spike
- Process Explorer can do the same

procdump -accepteula

## Process Explorer

- top windows shows list of currently active processes
- Bottom window if handle mode: see handles that process selected in top windows open. if in DLL mode: see DLLs and memory mapped files that the process has loaded

procexp -accepteula

## **Process Monitor**

- Process Monitor is an advanced monitoring tool for Windows that shows real-time file system, Registry and process/thread activity. It combines the features of two legacy Sysinternals utilities, Filemon and Regmon

procmon -accepteula

## PsExec

- lightweight telnet replacement that lets you execute processes on other systems, complete with full interactivity for console applications without having to manually install client software.
- launch interactive command-prompts opn remote systems and remote-enabling tools like opconfig that otherwise do not have the ability to show info about remote systems
- used by adversaries

psexec -accepteula

# Security utilities

## sysmon

- Monitor and log system activity to the windows event log.
- provides detailed info about process creations,network connections and changes to file creation time.

# System information

## WindObj

- uses native Windows NT API to access and display information on the NT object manager’s name space

winobj -accepteula

- Session 0 is the OS session and Session 1 is the User session
- atleast 2 csrss.exe processes running

# Miscellaneous

## BGInfo

- automatically displays relevant information about a windows computer on the desktop’s background, such as computer name, ip address, service pack version and more
- typically used on serers
- when a user RDp into server, the sys info is displayed on the wallpaper to proide quick info about the server such as server name

## RegJump

- takes a r egistry path and makes regedit open to that path. it accepts root keys in standard eg: HKEY_LOCAL_MAHINE and abbrevieated form HKLM

regjump -accepteula

- opens the reg editor and auto opens t he editor directly at the path, so one doesnt need to navigate it manually.

## Strings

- scans for unicode or ascii strings of a default length of 3 or more chars

C:\Users\Administrator\Desktop\SysinternalsSuite>strings ZoomIt.exe | findstr /i pdb*
D:\a\1\s\Win32\Release\ZoomIt.pdb
D:\a\1\s\x64\Release\ZoomIt64.pdb