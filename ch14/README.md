# Chapter 14: Network Operations

## IP Addresses
- Devices attached to a network must have at least one unique network address identifier known as the IP (Internet Protocol) address
- Exchanging information across the network requires using streams of small packets, each of which contains a piece of the information going from one machine to another.
- These packets contain data buffers, together with headers which contain information about where the packet is going to and coming from, and where it fits in the sequence of packets that constitute the stream.
- IPv4 uses 32-bits for addresses; there are only 4.3 billion unique addresses available. An IPv4 address is divided into four 8-bit sections called octets.
- One reason IPv4 has not disappeared is there are ways to effectively make many more addresses available by methods such as NAT (Network Address Translation).
- NAT enables sharing one IP address among many locally connected computers, each of which has a unique address only seen on the local network.

## IP Address Allocation
- Typically, a range of IP addresses are requested from your Internet Service Provider (ISP) by your organization's network administrator
- You can assign IP addresses to computers over a network either manually or dynamically
- The Dynamic Host Configuration Protocol (DHCP) is used to assign IP addresses

## Name Resolution
- Name Resolution is used to convert numerical IP address values into a human-readable format known as the hostname.
- You can view your system’s hostname simply by typing `hostname` with no argument.
- The special hostname `localhost` is associated with the IP address 127.0.0.1

## Network Interfaces
- Network interfacesa are a connection channel between a device and a network
- Physically, network interfaces can proceed through a network interface card (NIC), or can be more abstractly implemented as software. You can have multiple network interfaces operating at once.
- Information about a particular network interface or all network interfaces can be reported by the `ip` and `ifconfig` utilities

```sh
# View the IP address
$ ip addr show

# View the routing information
$ ip route show

# Check the status of a remote host
$ ping -c 5 google.com
```

- A network requires the connection of many nodes. Data moves from source to destination by passing through a series of routers and potentially across multiple networks
- Servers maintain routing tables containing the addresses of each node in the network.
- The IP routing protocols enable routers to build up a forwarding table that correlates final destinations with the next hop addresses.

Task | Command
--- | ---
Show current routing table | `$ route –n or ip route`
Add static route | `$ route add -net address or ip route add`
Delete static route | `$ route del -net address or ip route del`

## traceroute
- `traceroute` is used to inspect the route which the data packet takes to reach the destination host, which makes it quite useful for troubleshooting network delays and errors.
- By using `traceroute`, you can isolate connectivity issues between hops, which helps resolve them faster.

## More Networking Tools

Networking Tools | Description
--- | ---
`ethtool` | Queries network interfaces and can also set various parameters such as the speed
`netstat` | Displays all active connections and routing tables. Useful for monitoring performance and troubleshooting
`nmap` | Scans open ports on a network. Important for security analysis
`tcpdump` | Dumps network traffic for analysis
`iptraf` | Monitors network traffic in text mode
`mtr` | Combines functionality of ping and traceroute and gives a continuously updated display
`dig` | Tests DNS workings. A good replacement for host and nslookup

## wget and curl
- `wget` is a command line utility that can capably handle the following types of downloads:
    - Large file downloads
    - Recursive downloads, where a web page refers to other web pages and all are downloaded at once
    - Password-required downloads
    - Multiple file downloads.
- `curl` also allows you to save the contents of a web page to a file

## Transferring files
- File Transfer Protocol (FTP) is a well-known and popular method for transferring files between computers
- `sftp` is a very secure mode of connection, which uses the Secure Shell (ssh) protocol
- Secure Shell (SSH) is a cryptographic network protocol used for secure data communication
- We can also move files securely using Secure Copy (scp) between two networked hosts. scp uses the SSH protocol for transferring data
- [Network troubleshooting example](https://courses.edx.org/asset-v1:LinuxFoundationX+LFS101x+1T2020+type@asset+block/labsol-network.html)

## Summary
- The IP (Internet Protocol) address is a unique logical network address that is assigned to a device on a network.
- IPv4 uses 32-bits for addresses and IPv6 uses 128-bits for addresses.
- Every IP address contains both a network and a host address field.
- There are five classes of network addresses available: A, B, C, D & E.
- DNS (Domain Name System) is used for converting Internet domain and host names to IP addresses.
- The `ifconfig` program is used to display current active network interfaces.
- The commands `ip addr show` and `ip route show` can be used to view IP address and routing information.
- You can use `ping` to check if the remote host is alive and responding.
- You can use the `route` utility program to manage IP routing.
- You can monitor and debug network problems using networking tools.
- Firefox, Google Chrome, Chromium, and Epiphany are the main graphical browsers used in Linux.
- Non-graphical or text browsers used in Linux are Lynx, Links, and w3m.
- You can use `wget` to download webpages.
- You can use `curl` to obtain information about URLs.
- FTP (File Transfer Protocol) is used to transfer files over a network.
- ftp, sftp, ncftp, and yafc are command line FTP clients used in Linux.
- You can use `ssh` to run commands on remote systems.
