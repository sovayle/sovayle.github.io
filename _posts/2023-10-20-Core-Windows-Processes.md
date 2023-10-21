---
title: "Core Windows Processes"
categories: knowledge
permalink: /blogs/core-windows-processes
toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
---

# Core Windows Processes

## Windows process tools

- Process Hacker
- Process Explorer

## ****Core Windows Processes****

### System (run only in kernel-mode)

- pid = 4
- no parent process
- session 0

**Image Path**: C:\Windows\system32\ntoskrnl.exe (NT OS Kernel)

**Parent Process**: System Idle Process (0)

What is unusual behaviour for this process?

- A parent process (aside from System Idle Process (0))
- Multiple instances of System. (Should only be one instance)
- A different PID. (Remember that the PID will always be PID 4)
- Not running in Session 0

### System’s smss.exe ( session manager subsystem)

- responsible for creating new sessions
- first user-mode process started by the kernel
- This subsystem includes win32k.sys (kernel mode), winsrv.dll (user mode), and csrss.exe (user mode).
- 

**Image Path**:  %SystemRoot%\System32\smss.exe

**Parent Process**:  System

**Number of Instances**:  One master instance and child instance per session. The child instance exits after creating the session.

**User Account**:  Local System

**Start Time**:  Within seconds of boot time for the master instance

What is unusual?

- A different parent process other than System (4)
- The image path is different from C:\Windows\System32
- More than one running process. (children self-terminate and exit after each new session)
- The running User is not the SYSTEM user
- Unexpected registry entries for Subsystem

## csrss.exe (Client Server Runtime Process)

- responsible for win32 console window & process thread creation and deletion
- For each instance, csrsrv.dll, basesrv.dll, and winsrv.dll are loaded (along with others).
- responsible for making windows API available for other processors
- handles windows shutdown process
- smss.exe calls this process and self-terminates

**Image Path**:  %SystemRoot%\System32\csrss.exe

**Parent Process**:  Created by an instance of smss.exe

**Number of Instances**:  Two or more

**User Account**:  Local System

**Start Time**:  Within seconds of boot time for the first two instances (for Session 0 and 1). Start times for additional instances occur as new sessions are created, although only Sessions 0 and 1 are often created.

What is unusual?

- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes masquerading as csrss.exe in plain sight
- The user is not the SYSTEM user.

## **wininit.exe**

- responsible for launchign services.exe (Service Control Manager), lsass.exe (Local Security Authority), and lsaiso.exe within Session 0

**Image Path**:  %SystemRoot%\System32\wininit.exe

**Parent Process**:  Created by an instance of smss.exe

**Number of Instances**:  One

**User Account**:  Local System

**Start Time**:  Within seconds of boot time

What is unusual?

- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM

## **Service Control Manager** (SCM) or **services.exe**

- handle system services: loading, interacting and start/end services
- maintains database queried using windows built in utility, sc.exe
- stored in the registry, `HKLM\System\CurrentControlSet\Services`
- is the parent of svchost.exe, spoolsv.exe, msmpeng.exe, and dllhost.exe
- 

**Image Path**:  %SystemRoot%\System32\services.exe

**Parent Process**:  wininit.exe

**Number of Instances**:  One

**User Account**:  Local System

**Start Time**:  Within seconds of boot time

What is unusual?

- A parent process other than wininit.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM

## under services.exe, svchost.exe

- HKLM\SYSTEM\CurrentControlSet\Services\SERVICE NAME\Parameters
- 

**Image Path**: %SystemRoot%\System32\svchost.exe

**Parent Process**: services.exe

**Number of Instances**: Many

**User Account**: Varies (SYSTEM, Network Service, Local Service) depending on the svchost.exe instance. In Windows 10, some instances run as the logged-in user.

**Start Time**: Typically within seconds of boot time. Other instances of svchost.exe can be started after boot.

- -k used for grouping similar services to share the same process
- this process has been a target for malicious use
- 

**Image Path**: %SystemRoot%\System32\svchost.exe

**Parent Process**: services.exe

**Number of Instances**: Many

**User Account**: Varies (SYSTEM, Network Service, Local Service) depending on the svchost.exe instance. In Windows 10, some instances run as the logged-in user.

**Start Time**: Typically within seconds of boot time. Other instances of svchost.exe can be started after boot.

What is unusual?

- A parent process other than services.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- The absence of the -k parameter

## lsass.exe

- Local Security Authority Subsystem Service (**LSASS**)
- responsible for enforcing the security policy on the system
- verify users logging on windows comp/server
- handles password changes
- creates access tokens ( SAM security account manager, AD, netlogon)
- writes windows security log
- 

**Image Path**:  %SystemRoot%\System32\lsass.exe

**Parent Process**:  wininit.exe

**Number of Instances**:  One

**User Account**:  Local System

What is unusual?

- A parent process other than wininit.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM

## Winlogon.exe

- Responsible for Secure Attention Sequence (SAS). it is ALT + CTRL + Del
- responsible for loading the user profile. it loads NTUSER.DAT into HKCU, and userinit.exe loads the user’s shell
- responsible for lockign the screen and screensaver
- 

**Image Path**:  %SystemRoot%\System32\winlogon.exe

**Parent Process**:  Created by an instance of smss.exe that exits, so analysis tools usually do not provide the parent process name.

**Number of Instances**:  One or more

**User Account**:  Local System

**Start Time**:  Within seconds of boot time for the first instance (for Session 1). Additional instances occur as new sessions are created, typically through Remote Desktop or Fast User Switching logons.

What is unusual?

- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Not running as SYSTEM
- Shell value in the registry other than explorer.exe

## explorer.exe

- start menu and taskbar and folder and files
- 

**Image Path**:  %SystemRoot%\explorer.exe

**Parent Process**:  Created by userinit.exe and exits

**Number of Instances**:  One or more per interactively logged-in user

**User Account**:  Logged-in user(s)

**Start Tim**e:  First instance when the first interactive user logon session begins

What is unusual?

- An actual parent process. (userinit.exe calls this process and exits)
- Image file path other than C:\Windows
- Running as an unknown user
- Subtle misspellings to hide rogue processes in plain sight
- Outbound TCP/IP connections
