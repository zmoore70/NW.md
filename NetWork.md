https://github.com/S-DeHerrera-Neil/Collaboration_Networking-Collab.md/tree/main
Network


SSH Usage

-p {port} - Alternate port
-l {username} - Specify the username
-X - Enable X11 forwarding
-v(vv) - Add logging and debugging
-i {identity file} - Specify a private key identity
-F {config file} - Specify an alternate user config file
-N - Do not send remote commands
-T - Do not create a pseudo vty
-C - Enable compression
-f - Backgroud process after authentication
-J user@host - Proxy jump
-L [bind_address:]port:host:hostport
-R [bind_address:]port:host:hostport
-D {port}

SSH Key Change Fix

ssh-keygen -f "/home/student/.ssh/known_hosts" -R "172.16.82.106"

  Copy/Paste the ssh-keygen message to remove the Host key from the known_hosts file

  When you re-connect it will prompt you to save the new Host key

# TCPdump

## -A - Prints the frame payload in ASCII.                                                                                                                      
```
- tcpdump -A
```
## -D - Print the list of the network interfaces available on the system and on which TCPDump can capture packets. For each network interface, a number and an interface name, followed by a text description of the interface, is printed. This can be used to identify which interfaces are available for traffic capture.                                                                                  
```
- tcpdump -D
```
## -i - Normally, eth0 will be selected by default if you do not specify an interface. However, if a different interface is needed, it must be specified.       
```
- tcpdump -i eth0
```
## -e - Prints Data-Link Headers. Default is to print the encapsulated protocol only.                                                                           
```
- tcpdump -e
```
## -X - displays packet data in HEX and ASCII.                                                                                                                  
```
- tcpdump -i eth0 -X
```
## -XX - displays the packet data in HEX and ASCII to include the Ethernet portion.                                                                             
```
- tcpdump -i eth0 -XX
```
## -w - writes the capture to an output file                                                                                                                    
```
- tcpdump -w something.pcap
```
## -r - reads from the pcap                                                                                                                                     
```
- tcpdump -r something.pcap
```
## -v - gives more verbose output with details on the time to live, IPID, total length, options, and flags. Additionally, it enables integrity checking.
```
- tcpdump -vv
```
## -n - Does not covert protocol and addresses to names                                                                                                         
```
-  tcpdump -n
```

## tcpdump for specific protocol traffic of more than one type.
```
tcpdump port 80 or 22 -vn
```
## tcpdump for a range of ports on 2 different hosts with a destination to a specific network
```
tcpdump portrange 20-100 and host 10.1.0.2 or host 10.1.0.3 and dst net 10.2.0.0/24 -vn
```
## tcpdump filter for source network 10.1.0.0/24 and destination network 10.3.0.0/24 or dst host 10.2.0.3 and not host 10.1.0.3.
```
tcpdump "(src net 10.1.0.0/24  && (dst net 10.3.0.0/24 || dst host 10.2.0.3) && (! dst host 10.1.0.3))"" -vn
```




# VIEW/CHANGE SSH PORT
```
To view the current configured SSH port

    cat /etc/ssh/sshd_config | grep Port

Edit file to change the SSH Port

    sudo nano /etc/ssh/sshd_config

Restart the SSH Service

    systemctl restart ssh
```
# Day 1

## 3.4.4.2 Explain DNS Records
```
A DNS servers contains a "zone file" for each domain, and the zone file is made up of "resource records" (RRs) which acts as instructions for the DNS server.

Common list of records are:

Type A

    IPv4 Address record, used to map hostnames to an IP address of the host.

Type AAAA

    IPv6 address record, used to map hostnames to an IPv6 address of the host.

Type MX

    Mail exchange record, Maps a domain name to a list of message transfer agents for that domain.

Type TXT

    Text record, human-readable text in a DNS record, but can also store machine-readable data. Often used for verification and authentication.

Type NS

    Name Server record, specifies the authoritative name servers for a domain.

Type SOA

    Start of authority, provides authoritative information about the zone, including administrative details and zone-level settings.

Type AXFR

    AXFR (Full Zone Transfer) facilitates the transfer of the entire DNS zone data, including all resource records, from one DNS server (the master) to another DNS server (the slave).

Type IXFR

    IXFR (Incremental Zone Transfer) Retrieves only the changes made since the last transfer.

Type CNAME

    Canonical Name creates an alias for a domain name, pointing it to another canonical domain.

Type PTR

    Used for reverse DNS lookups to map an IP address to a domain name.

A extended list of records can be found here: DNS record types

Linux command to view records: dig
Example: dig stackoverflow.com

Windows command to view records: ipconfig /displaydns
```
## Below are a series of all the folders and commands you will use in this course.

    1. To view your IP address and interface information:
        a. current =        ip address (ip addr)
        b. deprecated =     ifconfig

    2. To view your ARP cache:
        a. current =        ip neighbor (ip nei)
        b. deprecated =     arp -a

    3. To view open TCP and UDP sockets:
        a. current = 
            i. TCP =        ss -antlp
            ii. UDP =       ss -anulp
        b. deprecated =     netstat

    4. To create, edit, or modify a file from the command line:
        a. vi =             vi <file>
        b. vim =            vim <file>
        c. nano =           nano <file>
    
    5. To view active processes:
        a. static =         ps -elf
        b. real-time =      top or htop

    6. To open file manager from the command line from X11 connection:
        a. nautilus
        b. pcmanfm

    7. Web Browsers from X11 connection:
        a. Firefox
        b. Chromium
        c. Konqueror

    8. To open images from the command line from X11 connection:
        a. Eye of Gnome =                   eog [file]
        b. Nomacs =                         nomacs [file]
        c. Eye of Mate =                    eom [file]
        d. GNU Image Manipulation Program = gimp [file]

    9. Find command:
        a. find / -iname <file pattern> 2>/dev/null
            / = starting location of search
            -iname = search for <file patter> with no case sensitivity
            <file pattern> = name of file to search for. Can use '*' as wildcards.
            2>/dev/null = send all errors to /dev/null

    10. Network scanning:
        a. nmap
            -sT = TCP Full connection
                nmap -sT 10.10.0.40 -p 21-23,80
            -sS = TCP SYN scanning
                sudo nmap -sS 10.10.0.40 -p 21-23,80
            -Pn = Disable ping sweep
                nmap -Pn -sT 10.10.0.40 -p 21-23,80
            -sU = UDP scanning
                sudo nmap -sU 10.10.0.40 -p 1000-2000
            -p- = Scan all ports
                nmap -sT 10.10.0.40 -p-
                nmap -sT 10.10.0.40 -p 1-65535
        b. zenmap
        c. netcat
            TCP: nc -nzvw1 10.10.0.40 21-23 80
            UDP: nc -unzvw1 10.10.0.40 53 69
        d. ping
            ping 10.10.0.40
        e. traceroute
            traceroute 172.16.82.106

    11. Network Utilization:
        a. iftop
        b. iptraf-ng

    12. Packet Manipulation (requires root privileges):
        a. scapy
        b. hping3
        c. yersinia     yersinia -G

    13. Packet Sniffing (requires root privileges):
        a. Wireshark
        b. tcpdump
        c. p0f
        d. tshark

    14. Banner Grabbing:
        a. netcat
            Client: nc 10.10.0.40 22
            Listener: nc -lvp 1234
        b. telnet
            telnet 10.10.0.40
            telnet 10.10.0.40 2323
            telnet localhost 1111
        c. wget
            wget -r http://10.10.0.40
            wget -r http://10.10.0.40:8080
            wget -r http://localhost:1111
            wget -r ftp://10.10.0.40
        d. curl
            curl http://10.10.0.40
            curl http://10.10.0.40:8080
            curl http://localhost:1111
            curl ftp://10.10.0.40

    15. DNS Query:
        a. whois
            whois google.com
        b. dig
            Records:
                A - IPv4
                    dig domain_name A
                AAAA - IPv6
                    dig domain_name AAAA
                NS - Name Server
                    dig domain_name NS
                SOA - Start of Authority
                    dig domain_name SOA
                MX - Mail Server
                    dig domain_name MX
                TXT - Human readable message
                    dig domain_name TXT
                AXFR - Zone Transfer
                    dig AXFR @dns_server domain_name

    16. Remote access:
        a. ssh
            ssh student@10.10.0.40
            ssh student@10.10.0.40 -p 2222
            ssh student@localhost -p 2222
        b. telnet
            telnet 10.10.0.40
            telnet 10.10.0.40 2323
            telnet localhost 1111

    17. File Transfer:
        a. scp
            scp student@10.10.0.40:/usr/share/cctc/flag.png .
            scp -P 2222 student@10.10.0.40:/usr/share/cctc/flag.png .
            scp -P 2222 student@localhost:/usr/share/cctc/flag.png .
            scp flag.png student@10.10.0.40:
            scp -P 2222 flag.png student@10.10.0.40:
            scp -P 2222 flag.png student@localhost:
        b. netcat
            nc 10.10.0.40 1234 < flag.png
            nc -lvp 1234 > flag.png
        c. ftp
            ftp 10.10.0.40
            
    18. Creating SSH Tunnels:
        a. Local Port Forward:
            ssh <user>@<server.ip> -p <alt port> -L <local bind port>:<tgt ip>:<tgt port>
        b. Remote Port Forward:
            ssh <user>@<server.ip> -p <alt port> -R <server bind port>:<tgt ip>:<tgt port>
        c. Dynamic:
            ssh <user>@<server.ip> -p <alt port> -D 9050

    19. To determine if tool or application is installed:
        a. which =              which <tool>
        b. whereis =            whereis <tool>

    20. Create a named pipe file:
        a. mknod =              mknod <file> -p
        b. mkfifo =             mkfifo <file>

    21. File and locations discussed in CCTC Networking:
        a. /etc/passwd =                List of user accounts
        b. /etc/shadow =                User password database
        c. /etc/services =              Services file
        d. /etc/os-release =            OS information
        e. /etc/ssh/ssh_config =        SSH user config 
        f. /etc/ssh/sshd_config =       SSH Daemon config
        g. ~/.ssh/known_hosts =         Public keys of all saved SSH servers
        h. /etc/snort =                 Snort directory
        i. /etc/snort/snort.conf  =     Snort config file
        j. /etc/snort/rules =           Default snort rules directory
        k. /var/log/snort =             Default snort log file directory
        l. /usr/share/cctc =            Default location of flags and files in shared environments
        m. /etc/proxychains.conf =      Proxychains config file
        n. /etc/p0f/p0f.fp =            p0f fingerprint file

    22. File descriptors:
        0 = Standard Input (STDIN)
        1 = Standard Output (STDOUT)
        2 = Standard Error (STDERR)
    
    23. Redirectors:
        > - redirect the STDOUT (1) of a command into a file.
            ls > file.txt
        >> - appends the STDOUT (1) of a command into a file. 
            echo "new data" >> file.txt
        < - redirect the STDOUT (1) of a file into a command.
            sort < input.txt
        | - redirect the STDOUT (1) of one command as STDIN (0) of another command.
            ps aux | grep ssh
        >& - redirect to a file descriptor.
            2>&1 | grep "open" - redirect STDERR(2) to STDOUT(1) the redirect the output to the command "grep"

## BPFs at the Data-Link layer
```
    Search for the destination broadcast MAC address.

'ether[0:4] = 0xffffffff && ether[4:2] = 0xffff'
'ether[0:2] = 0xffff && ether[2:2]= 0xffff && ether[4:2] = 0xffff'

    Search for the source MAC address of fa:16:3e:f0:ca:fc.

'ether[6:4] = 0xfa163ef0 && ether[10:2] = 0xcafc'
'ether[6:2] = 0xfa16 && ether[8:2] = 0x3ef0 && ether[10:2] = 0xcafc'
```
##     Search for unicast (0x00) or multicast (0x01) MAC address.
```
'ether[0] & 0x01 = 0x00'
'ether[0] & 0x01 = 0x01'
'ether[6] & 0x01 = 0x00'
'ether[6] & 0x01 = 0x01'
```
## Search for IPv4, ARP, VLAN Tag, and IPv6 respectively.
```
ether[12:2] = 0x0800
ether[12:2] = 0x0806
ether[12:2] = 0x8100
ether[12:2] = 0x86dd
```
##     Search for 802.1Q VLAN 100.
```
'ether[12:2] = 0x8100 && ether[14:2] & 0x0fff = 0x0064'
'ether[12:4] & 0xffff0fff = 0x81000064'
```
## Search for double VLAN Tag.
```
'ether[12:2] = 0x8100 && ether[16:2] = 0x8100'
```
## Search for ONLY the RES flag set. DF and MF must be off.
```
'ip[6] & 0xE0 = 0x80'
'ip[6] & 224 = 128'
```
## Search for RES bit set. The other 2 flags are ignored so they can be on or off.
```
'ip[6] & 0x80 = 0x80'
'ip[6] & 128 = 128'
```
# Day 2

# Hex Encoding and Decoding

## Encode text to Hex:
```
echo "Message" | xxd
```
## Encode file to Hex:
```
xxd file.txt file-encoded.txt
```
## Decode file from Hex:
```
xxd -r file-encoded.txt file-decoded.txt
```
# Base64 Encoding and Decoding

## Encode text to base64:
```
echo "Message" | base64
```
## Endode file to Base64:
```
base64 file.txt > file-encoded.txt
```
## Decode file from Base64:
```
base64 -d file-encoded.txt > file-decoded.txt
```
# md5sum
```
echo "Message" | md5sum
```
# DAY 3
## Good Sites
```
http://whois.domaintools.com/
https://centralops.net/co/
https://urlscan.io/
https://web-check.xyz/
https://iplocation.io/
https://bgpview.io/
duckduckgo
https://app.diagrams.net/
```
# Commands for Passive Recon
## WHOIS
```
whois zonetransfer.me
```
## Dig
```
dig zonetransfer.me A
dig zonetransfer.me AAAA
dig zonetransfer.me MX
dig zonetransfer.me TXT
dig zonetransfer.me NS
dig zonetransfer.me SOA
```
## Zone Transfer
```
Between Primary and Secondary DNS over TCP port 53

https://digi.ninja/projects/zonetransferme.php

dir axfr {@soa.server} {target-site}
dig axfr @nsztm1.digi.ninja zonetransfer.me
```
## Historical Content
```
    Wayback Machine

    http://archive.org/web/
```
# p0f: Passive scanning of network traffic and packet captures.
```
more /etc/p0f/p0f.fp

sudo p0f -i eth0

sudo p0f -r test.pcap - READ PCAPS
```
# Commands
## Ping
```
Ping one IP:
ping 172.16.82.106 -c 1

Ping a range:
for i in {1..254}; do (ping -c 1 172.16.82.$i | grep "bytes from" &) ; done
```
## NMAP Defaults
```
Default Scan:

User: TCP Full Connect Scan (-sT)

Root: TCP SYN Scan (-sS)

Default Ports scanned: 1000 most commonly used TCP or UDP ports
```
## NMAP Options
```
    Broadcast Ping/Ping sweep (-sP, -PE)
    SYN scan (-sS)
    Full connect scan (-sT)
    Null scan (-sN)
    FIN scan (-sF)
    XMAS tree scan (-sX)
    UDP scan (-sU)
    Idle scan (-sI)
    Decoy scan (-D)
    ACK/Window scan (-sA)
    RPC scan (-sR)
    FTP scan (-b)
    OS fingerprinting scan (-O)
    Version scan (-sV)
    Discovery probes
    -PE - ICMP Ping
    -Pn - No Ping *Required during tunneling
```
## recon
Passive OS Fingerprinter (p0f)

    Examine packets sent to/from target

    Can guess Operating Systems and version

    Can guess client/server application and version

Social Tactics

    Social Engineering (Hack a person)

    Technical based (Email/SMS/Bluetooth)

    Other Types (Dumpster Diving/Shoulder Surf)

NMAP - Rate Limit

    --min-rate <number> - Minimum packets per second

    --max-rate <number> - Max packets per second

Traceroute - Firewalking

traceroute 172.16.82.106
traceroute 172.16.82.106 -p 123
sudo traceroute 172.16.82.106 -I
sudo traceroute 172.16.82.106 -T
sudo traceroute 172.16.82.106 -T -p 443

Netcat - Scanning

nc [Options] [Target IP] [Target Port(s)]

    -z : Port scanning mode i.e. zero I/O mode

    -v : Be verbose [use twice -vv to be more verbose]

    -n : do not resolve ip addresses

    -w1 : Set time out value to 1

    -u : To switch to UDP
  
  Netcat - Banner Grabbing

  Find what is running on a particular port

nc [Target IP] [Target Port]
nc 172.16.82.106 22
nc -u 172.16.82.106 53

    -u : To switch to UDP

  ## CURL AND WGET
  ```
        Both can be used to interact with the HTTP, HTTPS and FTP protocols.

    Curl - Displays ASCII

curl http://172.16.82.106
curl ftp://172.16.82.106

    Wget - Downloads (-r recursive)

wget -r http://172.16.82.106
wget -r ftp://172.16.82.106

if ssh or http are unavailable use ftp
ftp 172.16.82.106 - log in through FTP server. after logging in as student must go into passive mode "passive" to get files from ftp server must do "get [filename]"
```
## IP Configuration
```
Windows: ipconfig /all
Linux: ip address (ifconfig depreciated)
VyOS: show interface
```
## DNS configuration
```
Windows: ipconfig /displaydns
Linux: cat /etc/resolv.conf
```
## ARP Cache
```
Windows: arp -a
Linux: ip neighbor (arp -a depreciated)
```
## Network connections

Windows: netstat
Linux: ss (netstat depreciated) (atlp)
```
Example options useful for both netstat and ss: -antp
a = Displays all active connections and ports.
n = No determination of protocol names. Shows 22 not SSH.
t = Display only TCP connections.
u = Display only UDP connections.
p = Shows which processes are using which sockets.
```
Windows: C:\Windows\System32\OpenSSH\sshd_config
Linux: /etc/ssh/sshd_config

find / -iname hint* 2> /dev/null
find / -iname flag* 2> /dev/null

## Routing Table

Windows: route print
Linux: ip route (netstat -r deprecated)
VyOS: show ip route

ARP Scanning

arp-scan --interface=eth0 --localnet

# METHODOLOGY

Host discovery
  Ruby ping sweep(if ping available)
    
    *script*
  
  nmap scan if no ping (check scan methodology)

port Discovery
  
  nmap (check scan methodology)
  
  nc scan script

Port validation
  
  banner grab using nc [ipaddr] [port]

follow-on actions based on ports found
  
  if 21 or 80 wget -r [ip addr] (or) wget -r ftp://[ip addr] (or) firefox
  
  if 22 or 23 CONNECT amd PASSIVE RECON
  
  if no 22 or 23 and you NEED to GET ON the box and you have port 21
    
    FTP [ipaddr] connects to FTP server
      
      passive
      
      ls
      
      get [file name]


Scan Methodology
  
  nmap -Pn [IP] -T4 -p 21-23,80
  
  quick scan ports 21-23,80
  
  specific ports based on hints/clues found 
  
  well known port range
  
  which tcpdump wireshark nmap telnet get curl ping

  
  0-1023
  
  Chunks of 2000 or first 10000 ports 
  
  Hail Mary - Scan all of the ports

  Passive recon:

hostname
  
  permissions:
    
    sudo -l

interfaces and subnets
    
    ip a
    
    show interface{VyOS}

neighbors
    
    ip neigh

Routing table
    
    ip route 
    
    show ip route

files  of interest
  
  find / -iname flag*
  
  find / -iname hint*

other listening ports
  
  ss -ntlp

available tools
  
  which tcpdump wireshark nmap telnet get curl ping

# SCP

## SCP Options
```
.  - Present working directory
-v - verbose mode
-P - alternate port
-r - recursively copy an entire directory
-3 - 3-way copy
```

## SCP Syntax
```
Download a file from a remote directory to a local directory
$ scp student@172.16.82.106:secretstuff.txt /home/student

Upload a file to a remote directory from a local directory
$ scp secretstuff.txt student@172.16.82.106:/home/student

Copy a file from a remote host to a separate remote host
$ scp -3 student@172.16.82.106:/home/student/secretstuff.txt student@172.16.82.112:/home/student
password:    password:
```
## SCP Syntax For Folders
```
Recursive upload of a folder to remote
$ scp -r folder/ student@172.16.82.106:

Recursive download of a folder from remote
$ scp -r student@172.16.82.106:folder/ .
```
## SCP Syntax through a tunnel
```
Create a local port forward to target device
$ ssh student@172.16.82.106 -L 1111:localhost:22 -NT

Download a file from a remote directory to a local directory
$ scp -P 1111 student@localhost:secretstuff.txt /home/student

Upload a file to a remote directory from a local directory
$ scp -P 1111 secretstuff.txt student@localhost:/home/student
```
## SSH Options
```
-L - Creates a port on the client mapped to a ip:port via the server     (LOCAL)

-D - Creates a port on the client and sets up a SOCKS4 proxy tunnel where the target ip:port is specified dynamically    (DYNAMIC)

-R - Creates the port on the server mapped to a ip:port via the client      (REMOTE)

-NT - Do not execute a remote command and disable pseudo-tty (will hang window)
```

![image](https://github.com/user-attachments/assets/a0e80886-c58c-40a4-a305-e4a841811853)

## Reverse examples
```
student@blue-internet-host-student-13:~$ ssh net2_student13@10.50.38.13 -p 1234 -L 21301:172.17.17.28:23 -NT --> (ssh to "Bender" and creates a local tunnel on BIH to go to "Philips" telnet) 

student@blue-internet-host-student-13:~$ telnet localhost 21301 (Telnet to the local fowarder to get onto Philips system)

net2_student13@philip:~$ ssh net2_student13@172.17.17.17 -p 1234 -R 21399:localhost:4321 -NT (ssh to "Benders" ssh port opening remote port 21399 to go to "Philips" ssh port)

student@blue-internet-host-student-13:~$ ssh net2_student13@10.50.38.13 -p 1234 -L 21302:localhost:21399 -NT (***COMBINING THE TUNNELS***)(ssh from BIH to "Bender" making a local fowarder on BIH to go to the 21399  on "Bender" which goes to "Philip" ssh port)

student@blue-internet-host-student-13:~$ ssh net2_student13@localhost -p 21302 -L 21303:192.168.30.150:1212 -NT (ssh to local fowarder going to "Leela" ssh port)

student@blue-internet-host-student-13:~$ ssh net2_student13@localhost -p 21303 -L 21304:10.10.12.121:2932 -NT (ssh to new local fowarder going to "Professors" ssh port while on target run commands to see high port then exit)

student@blue-internet-host-student-13:~$ ssh net2_student13@localhost -p 21304 (ssh to local fowarder that goes to professor. while on professor run commands to identify high port)

student@blue-internet-host-student-13:~$ ssh net2_student13@localhost -p 21304 -D 9050 -NT ( Creates a dynamic tunnel onto "Professor" then in new terminal run proxychains nc localhost *[port]* to view message on high port) 

```
# iptables syntax

## iptables -t [table] [options] [chain] [rules] -j [action]

## -t [table] can be filter(default), nat, mangle, raw or security

## Common iptable [options]:
```
-A, --append - Append a rule. Rule will be created at the end of the list or below the rule number you specify.
-I, --insert - Insert a rule. Rule will be created at the top of the list or above the rule number you specify.
-R, --replace - Replace a rule. The rule number your specify will be replaced with this rule.
-D, --delete - Delete a rule. The rule number you specify will be deleted.
-F, --flush - Flush the table of all rules.
-L, --list - List all rules in the specified table.
-S, --list-rules - Prints the rules in the specified table.
-P, --policy - Set the policy for the chain.
-n, --numeric - IP addresses and port numbers will be printed in numeric format.
-L --line-numbers - When listing rules, add line numbers to the beginning of each rule, corresponding to that rule's position in the chain.
```
## [chain] - Can be PREROUTING, INPUT, FORWARD, OUTPUT, or POSTROUTING

## [rules]
```
-i [iface] - Specifies the input interface
-o [iface] - Specifies the output interface
-s [ip.add | network/mask] - Specifies the source IP
-d [ip.add | network/mask] - Specifies the destination IP
-p [tcp | udp | icmp] - Specifies the protocol.
-p [tcp | udp] --sport [port | port1:port2] - Specifies the source port(s). Can be one port or one range.
-p [tcp | udp] --dport [port | port1:port2] - Specifies the destination port(s). Can be one port or one range.
-p icmp --icmp-type type# { /code# }  - Specifies specific icmp types and codes
-p tcp --tcp-flags SYN,ACK,PSH,RST,FIN,URG,ALL,NONE  - Specifies specific one or more TCP flags to filter on.

-m is used to call functions from iptables extensions:
-m state --state [state] - Enables stateful packet tracking. States can be NEW,ESTABLISHED,RELATED,UNTRACKED,INVALID
-m conntrack --ctstate [state] - Enables stateful packet tracking. States can be NEW,ESTABLISHED,RELATED,UNTRACKED,INVALID
-m mac --mac-source [mac]
       --mac-destination [mac]
-m multiport -p [tcp | udp] --sports [port1,port2,..port15] - Specifies the source port(s). Can be one port, one range, or
                                                             comma delimited.
                            --dports [port1,port2,..port15] - Specifies the destination port(s). Can be one port, one range, or
                                                             comma delimited.
                            --ports [port1,port2,..port15]  - Specifies the port(s). Can be one port, one range, or comma delimited.
                                                             Ports imply source or destination.
-m bpf --bytecode "bytecode" - Specify a Berkeley Packet Filter (BPF) bytecode filter as a matching criteria for filtering
                               network packets.
-m iprange --src-range { ip1-ip2 } - Specifies a range of source IPs.
           --dst-range { ip1-ip2 } - Specifies a range of destination IPs.

-j [action] - ACCEPT, REJECT, or DROP
```
# NFTables rule examples

  ## Creating a table
```
  nft add table ip CCTC
```
  ## Creating chains
```
    nft add chain ip CCTC INPUT { type filterhook input priority 0 \; policy accept \;}
    nft add chain ip CCTC OUTPUT { type filter hook output priority 0 \; policy accept \;}

    Specify an interface

    nft add rule ip CCTC INPUT iif eth0 accept
    nft add rule ip CCTC OUTPUT oif eth1 accept

    Specify an IP address

    nft add rule ip CCTC INPUT ip saddr 10.10.0.40 accept
    nft add rule ip CCTC OUTPUT ip daddr 10.10.0.40 accept

    Specify a network

    nft add rule ip CCTC INPUT ip saddr 10.10.0.32/27 accept
    nft add rule ip CCTC OUTPUT ip daddr 10.10.0.32/27 accept

    Specify a TCP ports as a server

    nft add rule ip CCTC INPUT tcp dport { 21-23, 80, 3389 } accept
    nft add rule ip CCTC OUTPUT tcp sport { 21-23, 80, 3389 } accept

    Specify a TCP ports as a client

    nft add rule ip CCTC OUTPUT tcp dport { 21-23, 80, 3389 } accept
    nft add rule ip CCTC INPUT tcp sport { 21-23, 80, 3389 } accept

    Specify a UDP ports as a server

    nft add rule ip CCTC INPUT udp dport { 53, 67-69 } accept
    nft add rule ip CCTC OUTPUT udp sport { 53, 67-69 } accept

    Specify a UDP ports as a client

    nft add rule ip CCTC OUTPUT udp dport { 53, 67-69 } accept
    nft add rule ip CCTC INPUT udp sport { 53, 67-69 } accept

    Specify inbound ICMP

    nft add rule ip CCTC INPUT icmp type 8 accept
    nft add rule ip CCTC OUTPUT icmp type 0 accept

    Specify outboud ICMP

    nft add rule ip CCTC OUTPUT icmp type 8 accept
    nft add rule ip CCTC INPUT icmp type 0 accept

    Specify TCP states

    nft add rule ip CCTC INPUT tcp dport { 21-23, 80, 3389 } ct state { new, established } accept
    nft add rule ip CCTC OUTPUT tcp sport { 21-23, 80, 3389 } ct state { new, established }  accept
```
# NETWORK
## prompt for standard acl configuration mode              action                source IP address            source wildcard
```
router(config)#                                    permit or deny            IP address or "any"          range from 0.0.0.0 to 255.255.255.255
                                                                                                          0.0.0.0 = host = exact match
                                                                                                          0.255.255.255 = IP address/8
                                                                                                          omit if source IP address is "any"
```
## Standard Numbered ACL Syntax
```
router(config)# access-list {1-99 | 1300-1999}  {permit|deny}  {source IP add}
               {source wildcard mask}

router(config)# access-list 10 permit host 10.0.0.1

router(config)# access-list 10 deny 10.0.0.0 0.255.255.255

router(config)# access-list 10 permit any
```
## Standard Named ACL Syntax
```
router(config)# ip access-list standard [name]

router(config-std-nacl)# {permit | deny}  {source ip add}  {source wildcard mask}

router(config)# ip access-list standard CCTC-STD

router(config-std-nacl)# permit host 10.0.0.1

router(config-std-nacl)# deny 10.0.0.0 0.255.255.255

router(config-std-nacl)# permit any
```
# Create access control entries for extended ACLs
```
action          Layer 3/4 protocol                  Source IP Address                  Source wildcard                                [operator] [port]

permit or deny      tcp/udp/icmp                    IP address or "any"           range from 0.0.0.0 to 255.255.255.255                lt - less than
                                                                                  0.0.0.0 = host = exact match                         gt - greater than
                                                                                  0.255.255.255 = IP address/8                         (n)eq - (not) equal
                                                                                  omit if source IP address is "any"                    icmp-type (and code)



Destination IP Address                      Destination wildcard                      [operator] [port]                              [Options]

IP address or "any"                  range from 0.0.0.0 to 255.255.255.255
                                    0.0.0.0 = host = exact match
                                    0.255.255.255 = IP address/8
                                    omit if source IP address is "any"
	

lt - less than
gt - greater than
(n)eq - (not) equal
range - of ports
icmp-type (and code)
	

including:
established
fragments
log(-input)
time-range
ttl
match-any
match-all
```
## Extended Numbered ACL Syntax
```
router(config)# access-list {100-199 | 2000-2699} {permit | deny} {protocol}
               {source IP add & wildcard} {operand: eq|lt|gt|neq}
               {port# |protocol} {dest IP add & wildcard} {operand: eq|lt|gt|neq}
               {port# |protocol}

router(config)# access-list 144 permit tcp host 10.0.0.0.1 any eq 22

router(config)# access-list 144 deny tcp 10.0.0.0 0.255.255.255 any eq 23

router(config)# access-list 144 permit icmp 10.0.0.0 0.255.255.255 192.168.0.0
               0.0.255.255 echo

router(config)# access-list 144 deny icmp 10.0.0.0 0.255.255.255 192.168.0.0
               0.0.255.255 echo echo-reply

router(config)# access-list 144 permit ip any any
```
## Extended Named ACL Syntax
```
router(config)# ip access-list extended  [name]

router(config-ext-nacl)# [sequence number] {permit | deny} {protocol}
                        {source IP add & wildcard} {operand: eq|lt|gt|neq}
                        {port# |protocol} {dest IP add & wildcard} {operand:
                        eq|lt|gt|neq} {port# |protocol}

router(config)# ip access-list extended CCTC-EXT

router(config-ext-nacl)# permit tcp host 10.0.0.0.1 any eq 22

router(config-ext-nacl)# deny tcp 10.0.0.0 0.255.255.255 any eq 23

router(config-ext-nacl)# permit icmp 10.0.0.0 0.255.255.255 192.168.0.0
                        0.0.255.255 echo

router(config-ext-nacl)# deny icmp 10.0.0.0 0.255.255.255 192.168.0.0
                        0.0.255.255 echo echo-reply

router(config-ext-nacl)# permit ip any any
```
# Snort Basics
## Snort Installation directory
```
        /etc/snort
```
  ## Snort Configuration file. Configuration files are used to define one or more rule files for packet matching. It uses the command include /path/name.rules to add rules to the configuration file. Several configuration files can be created for different Snort instances. Use the -c config-file to specify the configuration file or rule.
```
        /etc/snort/snort.conf
```
 ##   Snort rules directory. Rule files can be created anywhere but this is the default location.
```
        /etc/snort/rules
```
##    Snort rule files. The functionality of Snort relies on its rules. They can be download from Snort or can be user-defined. Generally, they are given the .rules extension to identify them as rule files but are not required.
```
        [name].rules
```
 ##   Snort Log directory. If not otherwise specified, all alerts and logs are created here. Other locations can be specified using the -l log-file.
```
        /var/log/snort
```
   ## Common Snort command line switches
```
        -D - Runs snort in Daemon mode

        -l log-dir - to specify the location where Snort should create its logs. If not specified then the default is /var/log/snort

        -c config-file - to specify a configuration or rule file that Snort should use for packet matching.

        -r pcap-file - to specify a pcap file for Snort to read.

        -p - Turn off promiscuous mode sniffing.

        -e - Display/log the link-layer packet headers.

        -i interface - Specify the interface for the Snort Daemon to sniff on.

        -V - Show the version number and exit.
```
  ##  To run snort as a Daemon
```
        sudo snort -D -c /etc/snort/snort.conf -l /var/log/snort
```
  ##  To run snort against a PCAP
```
        sudo snort -c /etc/snort/rules/file.rules -r file.pcap
```
# Snort IDS/IPS rule - header
Snort rules consist of a header which sets the conditions for the rule to work and rule options (a rule body) which provides the actual rule (matching criteria and action).
## [action] [protocol] [source ip] [source port] [direction] [destination ip] [destination port] ( match conditions ;)

A Snort header is composed of:
```
    Action - such as alert, log, pass, drop, reject

        alert - generate alert and log packet

        log - log packet only

        pass - ignore the packet

        drop - block and log packet

        reject - block and log packet and send TCP message (for TCP traffic) or ICMP message (for UDP traffic)

        sdrop - silent drop - block packet only (no logging)

    Protocol

        tcp

        udp

        icmp

        ip

    Source IP address

        a specific address (i.e. 192.168.1.1 )

        a CIDR notation (i.e. 192.168.1.0/24 )

        a range of addresses (i.e. [192.168.1.1-192.168.1.10] )

        multiple addresses (i.e. [192.138.1.1,192.168.1.10] )

        variable addresses (i.e. $EXTERNALNET ) (must be defined to be used)

        "any" IP address

    Source Port

        one port (i.e. 22 )

        multiple ports (i.e. [22,23,80] )

        a range of ports (i.e. 1:1024 = 1 to 1024, :1024 = less than or equal to 1024, 1024: = greater than or equal to 1024)

        variable ports (i.e. $EXTERNALPORTS) (must be defined to be used)

        any - When icmp protocol is used then "any" must still be used as a place holder.

    Direction

        source to destination ( - > )

        either direction ( <> )

    Destination IP address

        a specific address (i.e. 192.168.1.1 )

        a CIDR notation (i.e. 192.168.1.0/24 )

        a range of addresses (i.e. [192.168.1.1-192.168.1.10] )

        multiple addresses (i.e. [192.138.1.1,192.168.1.10] )

        variable addresses (i.e. $EXTERNALNET ) (must be defined to be used)

        "any" IP address

    Destination port

        one port (i.e. 22 )

        multiple ports (i.e. [22,23,80] )

        a range of ports (i.e. 1:1024 = 1 to 1024, :1024 = less than or equal to 1024, 1024: = greater than or equal to 1024)

        variable ports (i.e. $INTERNALPORTS) (must be defined to be used)

        any - When icmp protocol is used then "any" must still be used as a place holder.
```
 ## Snort IDS/IPS General rule options:
```
    msg - specifies the human-readable alert message. This only adds the message to the alert file.

        msg:"Put this message in the log";

    reference - links to external source of the rule. This just adds references to the attack the rule is filtering for.

        reference:cve,CAN-2000-1574;

    sid - used to uniquely identify Snort rules. This is required and all rules must have a unique sid.

        sid:123456;

    rev - uniquely identify revisions of Snort rules. This is purely for the administrator.

        rev: 1.1;

    Classtype - used to categorize a rule as detecting an attack that is part of a more general type of attack class. Classtypes must be defined before they can be used.

        classtype:attempted-recon;

    priority - assigns a severity level to rules (1 - really bad, 2 - badish, 3 - informational).

        priority:10;

    metadata - allows a rule writer to embed additional information about the rule.

        metadata:engine shared,service http;
```




