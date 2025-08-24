# Network-Scanning-NMAP
What is NMAP
Network Mapper (Nmap) is a network scanning and host detection tool that is very useful during several  steps  of penetration testing. Nmap is not limited to merely gathering information and enumeration, but it is also a powerful utility that can be used as a vulnerability detector or a security scanner.

What does NMAP do?
So Nmap is  a  multipurpose tool,  and it  can  be run  on  many different  operating systems, including Windows, Linux, BSD and Mac. Nmap is a very powerful utility that can be used to
Detect the live host on the network (host discovery)
Detect the open ports on the host (port discovery or enumeration)
Detect the software and the version to the respective port (service discovery)
Detect the operating system, hardware address and software version
Detect the vulnerability and security holes (Nmap scripts)

Commands for basic scan
Ping scan 
Scans the list of devices up and running on a given subnet
ping scan ----> nmap -sp <ip address>

Stealth scan 
Stealth scanning is performed by sending an SYN packet and analyzing the response. If SYN/ACK is received, it means the port is open, and you can open a TCP connection
stealth scan ----> nmap -sS <ip address>

Version scan
Finding application versions is a crucial part in penetration testing. It makes your life easier since you can find an existing vulnerability from the Common Vulnerabilities and Exploits (CVE) database for a particular version of the service. You can then use it to attack a machine using an exploitation tool like Metasploit
version scan ----> nmap -sV <ip address>

OS scan
In addition to the services and their versions, Nmap can provide information about the underlying operating system using TCP/IP fingerprinting. Nmap will also try to find the system uptime during an OS scan.
nmap -sV <ip address>

Aggressive scan
Nmap has an aggressive mode that enables OS detection, version detection, script scanning, and traceroute. You can use the -A argument to perform an aggressive scan
nmap -A <ip address>

ARP scan
nmap -PR -sn <ip address>
arp-scan --localnet
sudo arp-scan -I eth0 -l

Scanning Multiple Hosts
Nmap has the capability of scanning multiple hosts simultaneously. This feature comes in real handy when you are managing vast network infrastructure.
You Can Scan Multiple Hosts Through Numerous Approaches:

Write all the IP addresses in a single row to scan all of the hosts at the same time.
nmap 192.164.1.1 192.164.0.2 192.164.0.2

Use the asterisk (*) to scan all of the subnets at once.
nmap 192.164.1.*

Add commas to separate the addresses endings instead of typing the entire domains.
nmap 192.164.0.1,2,3,4

Use a hyphen to specify a range of IP addresses
nmap 192.164.0.0–255

Port Scanning
Port scanning is one of the most fundamental features of Nmap. You can scan for ports in several ways.
Using the -p param to scan for a single port
nmap -p 973 192.164.0.1

PING SWEEP
Ping sweep sends an ICMP packet to each possible IP address for the specified network. When it receives a response, it marks the IP address that responded as being alive. 

nmap -sn <ip address ranges or subnet mask>
nmap -PE -sn <ip address>

If you specify the type of port, you can scan for information about a particular type of connection, for example for a TCP connection.
nmap -p T:7777, 973 192.164.0.1

A range of ports can be scanned by separating them with a hyphen.
nmap -p 76–973 192.164.0.1

You can also use the -top-ports flag to specify the top n ports to scan.
nmap --top-ports 10 scanme.nmap.org

Scanning from a File
If you want to scan a large list of IP addresses, you can do it by importing a file with the list of IP addresses.
nmap -iL /input_ips.txt

The above command will produce the scan results of all the given domains in the “input_ips.txt” file. Other than simply scanning the IP addresses, you can use additional options and flags as well.
Verbosity and Exporting Scan Results
Penetration testing can last days or even weeks. Exporting Nmap results can be useful to avoid redundant work and to help with creating final reports. Let’s look at some ways to export Nmap scan results.

Verbose Output
nmap -v scanme.nmap.org
The verbose output provides additional information about the scan being performed. It is useful to monitor step-by-step actions Nmap performs on a network, especially if you are an outsider scanning a client’s network.

Normal output
Nmap scans can also be exported to a text file. It will be slightly different from the original command line output, but it will capture all the essential scan results.
nmap -oN output.txt scanme.nmap.org

XML output
Nmap scans can also be exported to XML. It is also the preferred file format of most pen-testing tools, making it easily parsable when importing scan results.
nmap -oX output.xml scanme.nmap.org

Multiple Formats
You can also export the scan results in all the available formats at once using the -oA command.
nmap -oA output scanme.nmap.org
The above command will export the scan result in three files — output.xml, output.Nmap and output.gnmap

Nmap Scripting Engine
Nmap Scripting Engine (NSE) is an incredibly powerful tool that you can use to write scripts and automate numerous networking features.
You can find plenty of scripts distributed across Nmap, or write your own script based on  your  requirements.  You  can  even  modify  existing  scripts  using  the  Lua programming language (https://en.wikipedia.org/wiki/Lua_(programming_language).

There are many categories available. Some useful categories include:

safe:- Won't affect the target
intrusive:- Not safe: likely to affect the target
vuln:- Scan for vulnerabilities
exploit:- Attempt to exploit a vulnerability
auth:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
brute:- Attempt to bruteforce credentials for running services
discovery:- Attempt to query running services for further information about the network (e.g. query an SNMP server).

Ok, so we know how to use the scripts in Nmap, but we don't yet know how to find these scripts.

We have two options for this, which should ideally be used in conjunction with each other. The first is the page on the Nmap website (mentioned in the previous task) which contains a list of all official scripts. The second is the local storage on your attacking machine. Nmap stores its scripts on Linux at /usr/share/nmap/scripts. All of the NSE scripts are stored in this directory by default -- this is where Nmap looks for scripts when you specify them.

There are two ways to search for installed scripts. One is by using the <cd /usr/share/nmap/scripts/script.db> <file script.db x head script.db> file. Despite the extension, this isn't actually a database so much as a formatted text file containing filenames and categories for each available script.

The second way to search for scripts is quite simply to use the ls command. For example, we could get the same results as in the previous screenshot by using ls -l /usr/share/nmap/scripts/*ftp*



