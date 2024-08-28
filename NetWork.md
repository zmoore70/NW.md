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


VIEW/CHANGE SSH PORT
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
