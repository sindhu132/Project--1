                                                                              Intrainz Project Submission     
                                                                      Footprinting with Nmap (Minor Project )
Introduction : 

•	Footprinting is the process of gathering information about a target or network. 
•	Nmap is a network exploration tool that can be used for footprinting.
•	 With Nmap, you can scan a target for open ports, services, operating systems, and other information.
•	Nmap also has many potential uses beyond footprinting, such as creating password crackers and network scanners.

Scanning the Target  : 


STEP-1 :  Identifying the target and start scanning with Nmap . 
	 Select the  target  nmap scanme.nmap.org 
	Enter the target in the linux terminal and start scanning .

                                           ┌──(sindhu_3531㉿Kali)-[~]
                                           └─$ nmap scanme.nmap.org      
                                            Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-31 11:48 IST
                                            Stats: 0:00:40 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
                                            Connect Scan Timing: About 68.80% done; ETC: 11:49 (0:00:14 remaining)
                                            Nmap scan report for scanme.nmap.org (45.33.32.156)
                                            Host is up (0.26s latency).
                                            Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
                                            Not shown: 996 closed tcp ports (conn-refused)
                                            PORT      STATE SERVICE
                                            22/tcp    open  ssh
                                            80/tcp    open  http
                                            9929/tcp  open  nping-echo
                                            31337/tcp open  Elite

                                            Nmap done: 1 IP address (1 host up) scanned in 53.73 seconds
                                                                                 
 
 

Step-2 :  Performing Service Version Detection on the Target.
	Version Detection is used with the -sV command, and it allows the user to collect information about the port. 
	This can include the version number, the service type, the operating system, the hostname, etc. 
	The following command is used for performing the service version detection network scanning (nmap –sV <target>)(nmap –sV scanme.nmap.org)


──(sindhu_3531㉿Kali)-[~]
└─$ nmap -sV scanme.nmap.org  
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-31 18:53 IST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.26s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 995 closed tcp ports (conn-refused)
PORT      STATE    SERVICE    VERSION
22/tcp    open     ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
80/tcp    open     http       Apache httpd 2.4.7 ((Ubuntu))
9929/tcp  open     nping-echo Nping echo
31337/tcp open     tcpwrapped
32782/tcp filtered unknown
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 56.35 seconds

 

Step-3 :  Performing OS detection Network scanning on the target
	Nmap OS detection is a quick and powerful way to determine what operating system a remote device is running.
	The following command is used for scanning the OS detection network scanning .
	That is  “Nmap –O <target> (example: nmap –O scanme.namp.org).

┌──(root㉿Kali)-[~]
└─# nmap -O scanme.nmap.org                        
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-31 18:55 IST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.27s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 996 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
9929/tcp  open  nping-echo
31337/tcp open  Elite
Aggressive OS guesses: Linux 2.6.32 (91%), Linux 2.6.32 or 3.10 (91%), Linux 3.5 (91%), Linux 4.2 (91%), WatchGuard Fireware 11.8 (91%), Synology DiskStation Manager 5.1 (91%), Linux 2.6.35 (90%), Linux 2.6.39 (90%), Linux 3.10 - 3.12 (90%), Linux 3.4 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 21 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 38.48 seconds
                                                                                
┌──(root㉿Kali)-[~]
└─# 


Step-4 :  Performing Aggressive scan on the target
	 Aggressive mode enables OS detection ( -O ), version detection ( -sV ), script scanning ( -sC ), and traceroute ( --traceroute ). 
	This mode sends a lot more probes, and it is more likely to be detected, but provides a lot of valuable host information.
	This scan mode can provide more detailed information about the systems and services installed on the target system, but it also requires more time and resources to run.
	To perform aggressive scanning we use the following command
	 Nmap –A <target> (nmap –A scanme.nmap.org)


┌──(root㉿Kali)-[~]
└─# nmap -A scanme.nmap.org
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-31 12:24 IST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.26s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 996 closed tcp ports (reset)-
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 ac:00:a0:1a:82:ff:cc:55:99:dc:67:2b:34:97:6b:75 (DSA)
|   2048 20:3d:2d:44:62:2a:b0:5a:9d:b5:b3:05:14:c2:a6:b2 (RSA)
|   256 96:02:bb:5e:57:54:1c:4e:45:2f:56:4c:4a:24:b2:57 (ECDSA)
|_  256 33:fa:91:0f:e0:e1:7b:1f:6d:05:a2:b0:f1:54:41:56 (ED25519)
80/tcp    open  http       Apache httpd 2.4.7 ((Ubuntu))
|_http-title: Go ahead and ScanMe!
|_http-favicon: Nmap Project
|_http-server-header: Apache/2.4.7 (Ubuntu)
9929/tcp  open  nping-echo Nping echo
31337/tcp open  tcpwrapped
Aggressive OS guesses: Linux 2.6.32 (92%), Linux 3.4 (91%), Linux 3.5 (91%), Linux 4.2 (91%), Linux 4.4 (91%), Synology DiskStation Manager 5.1 (91%), Linux 2.6.35 (90%), Linux 3.10 (90%), Linux 2.6.32 or 3.10 (90%), Linux 2.6.39 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 21 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 3389/tcp)
HOP RTT       ADDRESS
1   3.20 ms   192.168.0.1
2   2.39 ms   RTKGW.bbrouter (192.168.1.1)
3   7.18 ms   110.235.231.8
4   22.22 ms  110.235.231.1
5   33.87 ms  144.48.72.1
56 ms   14.142.71.93.static-hydrabad.vsnl.net.in (14.142.71.93)
43.77 ms  172.25.81.134
 28.08 ms  ix-ae-0-100.tcore1.mlv-mumbai.as6453.net (180.87.38.5)
  ...
 216.77 ms if-ae-12-2.tcore1.l78-london.as6453.net (180.87.39.21)
  ...
  241.27 ms ae13.r01.ewr01.icn.netarch.akamai.com (23.32.63.214)
 261.14 ms ae19.r01.ord01.icn.netarch.akamai.com (23.193.113.37)
 ...
 261.30 ms ae4.r02.sjc01.icn.netarch.akamai.com (23.32.63.27)
 ...
 261.41 ms a23-203-158-53.deploy.static.akamaitechnologies.com (23.203.158.53)
 270.24 ms 10.203.32.4
 277.42 ms 10.203.35.71
  ...
 261.73 ms scanme.nmap.org (45.33.32.156)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.09 seconds
                                                                                                                                                                                                      
┌──(root㉿Kali)-[~]
└─# 



 
Step-5 : Performing Scripting Scanning on the target (-sC)
	 Script scanning is a technique used in Nmap to execute predefined scripts against target systems to gather various types of information. 
	These scripts are written in the Lua programming language and are designed to probe specific services, operating systems, and applications. 
	Nmap script scanning can help identify vulnerabilities, misconfigurations , and potential security risks in target systems.
	To perform scripting scanning we use the following command.
	Nmap –sC <target> (nmap –sC scanme.nmap.org)


──(root㉿Kali)-[~]
└─# nmap -sC scanme.nmap.org
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-31 18:56 IST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.26s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 996 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
| ssh-hostkey: 
|   1024 ac:00:a0:1a:82:ff:cc:55:99:dc:67:2b:34:97:6b:75 (DSA)
|   2048 20:3d:2d:44:62:2a:b0:5a:9d:b5:b3:05:14:c2:a6:b2 (RSA)
|   256 96:02:bb:5e:57:54:1c:4e:45:2f:56:4c:4a:24:b2:57 (ECDSA)
|_  256 33:fa:91:0f:e0:e1:7b:1f:6d:05:a2:b0:f1:54:41:56 (ED25519)
80/tcp    open  http
|_http-favicon: Nmap Project
|_http-title: Go ahead and ScanMe!
9929/tcp  open  nping-echo
31337/tcp open  Elite

Nmap done: 1 IP address (1 host up) scanned in 78.62 seconds
                                                                                
┌──(root㉿Kali)-[~]
└─# 

 
Step-6 : Performing traceroute scanning on the target.(--script)
	Script scanning is a technique used in Nmap to execute predefined scripts against target systems to gather various types of information.
	 These scripts are written in the Lua programming language and are designed to probe specific services, operating systems, and applications. 
	Nmap script scanning can help identify vulnerabilities, misconfigurations, and potential security risks in target systems.
	To perform script scanning we use the following command .
	Nmap –script<target> (nmap –script scanme.nmap.org)

──(root㉿Kali)-[~]
└─# nmap --traceroute scanme.nmap.org
Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-31 19:03 IST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.29s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 996 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
9929/tcp  open  nping-echo
31337/tcp open  Elite

TRACEROUTE (using port 3306/tcp)
HOP RTT       ADDRESS
1   46.01 ms  192.168.0.1
2   45.97 ms  RTKGW.bbrouter (192.168.1.1)
3   47.16 ms  110.235.231.8
4   47.71 ms  110.235.231.1
5   47.24 ms  144.48.72.1
6   8.74 ms   14.142.71.93.static-hydrabad.vsnl.net.in (14.142.71.93)
7   ...
8   37.59 ms  ix-ae-0-100.tcore1.mlv-mumbai.as6453.net (180.87.38.5)
9   ... 10
11  214.71 ms if-ae-66-2.tcore3.nto-newyork.as6453.net (80.231.130.106)
12  218.74 ms ae13.r01.ewr01.icn.netarch.akamai.com (23.32.63.214)
13  233.59 ms ae19.r01.ord01.icn.netarch.akamai.com (23.193.113.37)
14  232.04 ms ae0.r02.ord01.icn.netarch.akamai.com (23.32.63.81)
15  271.69 ms ae4.r02.sjc01.icn.netarch.akamai.com (23.32.63.27)
16  271.67 ms ae2.r12.sjc01.ien.netarch.akamai.com (23.207.232.41)
17  271.65 ms a23-203-158-53.deploy.static.akamaitechnologies.com (23.203.158.53)
18  263.18 ms 10.203.32.4
19  259.09 ms 10.203.35.71
20  285.16 ms 10.203.7.43
21  259.64 ms scanme.nmap.org (45.33.32.156)

Nmap done: 1 IP address (1 host up) scanned in 48.08 seconds
                                                                                
┌──(root㉿Kali)-[~]
└─# 


 
