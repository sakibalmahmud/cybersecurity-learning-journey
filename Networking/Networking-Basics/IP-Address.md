# IP Address

An IP address (Internet Protocol address) is a number that identifies a device on a network.

Think of it like a home address: data needs to know where to go and where it came from.

**It has two main jobs:**

* **Identification:** Which device is this?
* **Location Addressing:** Where is this device on the network?

---

## IPv4

* The older and still most used version.
* **Size:** 32 bits, written as 4 numbers separated by dots.
* Each number is between 0 and 255.
* Example: `192.168.1.10`
* Total possible addresses: about 4.3 billion.
* Problem: The world ran out of free IPv4 addresses because there are more devices than available addresses.

## IPv6

* The newer version, made to solve the shortage of IPv4 addresses.
* **Size:** 128 bits, written as 8 groups of hexadecimal numbers separated by colons.
* Example: `2001:0db8:0000:0000:0000:0000:0000:0001`

**Shortening Rules:**

* Remove leading zeros in a group.
* Replace one run of all-zero groups with `::` (only once per address).
* The example above becomes `2001:db8::1`.

**Important Points:**

* Total addresses: Practically unlimited.
* No broadcast in IPv6 (it uses multicast instead).
* Loopback address: `::1`
* Link-local address starts with `fe80::`

---

## Public IP vs Private IP

### Public IP

* Unique on the whole internet.
* Given by your ISP (Internet Service Provider).
* Websites and servers generally see this one.

### Private IP

* Used inside a home, school or office network.
* Only unique inside that local network, so many different networks can reuse the same ones.
* Cannot be reached directly from the internet through normal public routing.

**Private IPv4 Ranges:**

* `10.0.0.0` to `10.255.255.255`
* `172.16.0.0` to `172.31.255.255`
* `192.168.0.0` to `192.168.255.255`

---

## NAT (Network Address Translation)

* Your router has one public IP, but many devices inside have private IPs.
* NAT lets all of them share that one public IP to use the internet.
* The router remembers which private device asked for what and sends the reply to the right one.
* Side effect: Outside people cannot normally reach your private devices directly, which provides some protection. However, NAT is not a replacement for a firewall.

---

## Dynamic IP vs Static IP

### Dynamic IP

* Assigned automatically (by the ISP or router) and can change over time.
* Most normal users have this.

### Static IP

* Configured to stay fixed until an administrator or ISP changes it.
* Usually costs extra when provided as a public IP by an ISP.
* Used for servers (websites, mail servers, CCTV, etc.), because other people must always find the same address.

---

## DHCP (Dynamic Host Configuration Protocol)

* DHCP gives IP addresses automatically to devices.
* When you connect to Wi-Fi, DHCP gives your device:

  * IP address
  * Subnet mask
  * Default gateway
  * DNS server

**The 4 steps are called DORA:**

1. **Discover:** The device asks, "Is there a DHCP server?"
2. **Offer:** The server offers an IP.
3. **Request:** The device says, "I will take it."
4. **Acknowledge:** The server confirms.

---

## Special IP Addresses

| IP Address        | Purpose                                                                                                               |
| ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| `127.0.0.1`       | Loopback or localhost: points to your own computer. Used for testing.                                                 |
| `0.0.0.0`         | Means an unspecified address; in some configurations, it represents all available IPv4 interfaces.                    |
| `169.254.x.x`     | APIPA: a device gives itself this when it cannot get an IP from DHCP. It usually indicates a DHCP or network problem. |
| `255.255.255.255` | Limited broadcast address for the local network segment.                                                              |

---

## Network Part and Host Part

**Every IP has two logical parts:**

* **Network Part:** Which network the device belongs to.
* **Host Part:** Which device or interface is inside that network.

The **subnet mask** shows where the split happens.

**Example:**

* IP Address: `192.168.1.10`
* Subnet Mask: `255.255.255.0`
* Network Address: `192.168.1.0`
* Host portion: `10`

In this example, the first 3 octets represent the network portion.

---

## CIDR (Slash Notation)

* A short way to write the subnet mask.
* `/24` means the first 24 bits are the network part, equivalent to `255.255.255.0`.
* Example: `192.168.1.0/24`

**Common CIDR Notations:**

| CIDR  | Subnet Mask     |
| ----- | --------------- |
| `/8`  | `255.0.0.0`     |
| `/16` | `255.255.0.0`   |
| `/24` | `255.255.255.0` |

**Calculating Usable IPv4 Hosts:**

For most conventional IPv4 subnets:

`Usable Hosts = 2^(Host Bits) - 2`

Example for `/24`:

* Host bits = 8
* `2^8 - 2 = 254` usable addresses.

We subtract 2 because one address is the network address and one is the broadcast address.

*Note: Special subnet sizes such as /31 and /32 have different rules.*

---

## Default Gateway

* The router's IP address inside your network in most home networks.
* When your device wants to reach something outside your local network, it sends the data to the gateway.
* Example: `192.168.1.1`

---

## Types of Communication

* **Unicast:** One device to one device (most common).
* **Broadcast:** One device to all devices in the network (IPv4).
* **Multicast:** One device to a selected group.
* **Anycast:** To one device among a group, typically the nearest according to routing.

---

## IP, MAC, Port and DNS (Do Not Mix Them Up)

* **IP Address:** Logical address that can change and works across networks.
* **MAC Address:** Data-link layer address of a network interface, used for local network communication.
* **Port:** Identifies which program or service on the device (example: 80 for HTTP, 443 for HTTPS, 22 for SSH).
* **DNS:** Converts domain names like `example.com` into IP addresses and provides other DNS records.

---

## ARP (Address Resolution Protocol)

* Finds the MAC address that belongs to an IPv4 address on the local network.
* Devices communicate on a local network using MAC addresses, so before sending data a device asks: "Who has this IP? Tell me your MAC address."
* Answers are saved in the **ARP table (cache)**.
* Check it with: `arp -a`
* IPv6 uses NDP (Neighbor Discovery Protocol) instead of ARP.

---

## Security Notes

* **Public IP Exposure:** Your public IP can show your approximate location (city or ISP), not usually your exact home address.
* **VPN:** A VPN routes your traffic through a VPN server. Websites generally see the VPN server's public IP.
* **IP Spoofing:** An attacker fakes the sender IP address.
* **Port Scanning:** Attackers check which ports are open on an IP (tools like Nmap).
* **ARP Spoofing:** An attacker sends fake ARP replies to trick devices on a local network.

**Security Reminder:** Only scan IP addresses and networks that you own or have explicit permission to test.

---

## Useful Commands

### Windows

| Command               | Purpose                                  |
| --------------------- | ---------------------------------------- |
| `ipconfig`            | Show IP configuration.                   |
| `ipconfig /all`       | Show full details (MAC, DNS, DHCP).      |
| `ping <ip or domain>` | Test connectivity.                       |
| `tracert <domain>`    | Show the route to a host.                |
| `nslookup <domain>`   | Find the IP of a domain.                 |
| `arp -a`              | Show the ARP table.                      |
| `netstat -ano`        | Show connections, ports and process IDs. |

### Linux (Kali Linux)

| Command               | Purpose                              |
| --------------------- | ------------------------------------ |
| `ip a`                | Show IP addresses.                   |
| `ip route`            | Show routes and the default gateway. |
| `ping <ip or domain>` | Test connectivity.                   |
| `traceroute <domain>` | Show the route to a host.            |
| `nslookup <domain>`   | Query DNS.                           |
| `dig <domain>`        | Perform DNS queries.                 |
| `ip neigh`            | Show the neighbor table.             |

---

## Hands-on Practice

Practice these commands on your own computer or an authorized lab environment.

1. Run `ipconfig /all` (or `ip a`). Is your IPv4 address private? Does it start with `192.168`, `10`, or `172.16–172.31`?
2. Find your default gateway.
3. Search "What is my IP" on the web. Compare it with your private IP.
4. Run `ping 127.0.0.1` and observe the reply.
5. Run `arp -a` or `ip neigh` and examine the entries.

---

**Next Topics to Learn:**

* Subnetting
* Public vs Private IP in Detail
* NAT and PAT
* DHCP
* IPv4 vs IPv6
