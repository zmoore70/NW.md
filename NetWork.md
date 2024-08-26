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

