---
title: "Basic Linux Commands"
categories: tools
permalink: /blogs/basic-linux-commands
#toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
---

## linux commands

- on linux mint (ubuntu based. which is debian based)
- on kali gnome install:
- sudo apt update
- sudo apt install stacer -y
- a thing
- whoami man clear ctrl l ctrl alt l pwd ls
- cd ~            or cd /
- rm -ri 
- cd ../..
- mkdir 
- touch (files) 
- rmdir
- rm -r
- ls zoo
- xdg-open .
- mv
- mv journal.txt journal_pro.txt
- mkdir Stuff, mv pie cake cookie Stuff
- cp -r (recursively)
- xdg-open (src) (dst)
- head tail -n
- date > (overwrite) >> (append)
- cat (concatanate and useful alongside >> (append) -n number
- less file( like man interface) with "/"(search smtg)
- echo "hi" [echo "testing echo" >> echoo.txt] cat echoo.txt
- wc word count

- piping | | | | redirects first command (output) as an input for second command ie; ls -l | wc       in this case ls -l is input 2nd command is wc
- sort
- uniq (used with sort) (piping) sort favFlavors.txt | uniq
- or sort -u favFlavors.txt
- or sort favFlavors.txt | uniq -d (duplicate) 
- or sort favFlavors.txt | uniq -c | (count) sort -nr numb rvrs
- echo $PATH / echo $USER
- echo *.txt (path)   / echo *.?? (?? can be .txt or whtvr like .py
- ls -l *.txt
- echo {a,b,c}.txt
- echo {a..z} prints a-z same with 1..100
- touch cow{1..4}.txt
- EXPANSIONS ^^^^ 
- diff -y or -u favFlavours1.txt favFlavours2.txt
- 24a25 append change delete
- find . -name '*.py*'
- grep -n
- du disk usage
- df disk info
- history
- ps process status
- top
- kill -l | less              15,9    kill -9 pid kill -15 pid
- killall -9 node
- jobs bg fg
- gzip -k keep the ori file
- gzip -d file (decompress)
- gunzip (unzip)
- tar (archive)
- tar -cf archive.tar file1 file2 file3 [NOT COMPRESSED]
- tar -tf archive.tar (view files but not unzipping them)
- tar -xf archive.tar (unzipping) xtract
- tar -czf bundle.tar file1 file2 file3 (zip n archived)
- nano file 
- ctrl k and u
- alias myls='ls -la' [non permanent]
- store in .bashrc if want permanent
- xargs [cat deadPlayers.txt | xargs rm]
- ln (link) a shortcut like a portal
- ln -s softlink.txt symlink.txt when ori is deleted, copy is ded
- who to see who is loged in
- su sudo
- passwd
- chown change own
- sudo chown colt Music
- regular file
- d directory
- l link
- c char special file
- rw- owner
- rw- group
- r-- world
- read write execute
- chmod [ chmod mode file ] [chmod g+w file.txt [a-w a+rwx a=r]
- ip a


## Kali update commands
- sudo apt-get update && apt-get upgrade
- apt install python-pip

- cd /opt ( place for downloads )
- git clone https://github.com/Dewalt-arch/pimpmykali.git
- cd /opt/pimpmykali
- ls
- ./pimpmykali.sh
- apt update && apt install mysql*
- tar filename
- tar -xf filename
- ```
- ./start-tor-browser.desktop --register-app

- ./start filename


## More Kali Commands
- ifconfig
- cat /etc/shadow [important. why]
- sudo su
- locate [locate bash]
- updatedb
- /tmp/ [quite useful when pentesting cus temp folder]
- chmod 777 hello.txt [(all permissions]
- adduser john
- /etc/passwd
- [use hashcat]  [go /etc/shadow file to crack the encrypted john passwd]
- su john[ssd]
- iwconfig [wireless adapter]
- ping ip
- arp -a
- netstat -ano [to see what's talking, to see if a machine is talking to smtg else, is it talking on smtg on a port]
- route [routing table]  [it tells where our traffic exits, the gateway is the place that it exits]
- ip a
- ip n [neighbour, arp]
- ip r
- apt update && apt upgrade [to update system. archive.linux is repository]
- apt install python-pip [pip for python]  [pip and pip3]
- [install smtg on github]  go cd /opt for downloads and stuff here, git clone ctrl shift v
- [how to run smtg?] ./ [pimpmykali.sh]


## 19/5 steganography

- binwalk
- exiftool- 
- exiftool <filename>
- cd exiftool
- ./exiftool /home/ladder/cat2.jpg
- jsteg
- steghide
