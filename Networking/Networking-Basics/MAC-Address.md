# MAC Address

It’s a unique, 12-character hardware identifier address used to identify a Network Interface Card (NIC) on a local network. It is usually assigned by the manufacturer. However, MAC addresses can be changed or randomized through software.

A MAC address is a 48-bit (6-byte) address, usually written in hexadecimal format.

**Example:**

`00:1A:2B:3C:4D:5E`

An interesting thing about MAC addresses is that they can be faked or "spoofed" in a process known as **MAC Spoofing**.

## How MAC Address Works

MAC addresses work at **Layer 2 (Data Link Layer)** of the OSI Model.

When devices communicate within the same local network (LAN), they use MAC addresses to deliver Ethernet frames to the correct network interface.

For example:

* IP Address helps identify where data needs to go.
* MAC Address helps deliver data to the correct device/interface within the local network.

When a device wants to communicate with another device on the same network, it uses ARP (Address Resolution Protocol) to find the destination MAC address using its IP address.

**Basic Mechanism:**

1. A device knows the destination IP address.
2. It checks its ARP table to see whether it already knows the destination MAC address.
3. If not, it sends an ARP Request to the local network.
4. The device with the matching IP address replies with its MAC address.
5. The sender uses that MAC address to deliver the Ethernet frame.

## Types of MAC Addresses

There are different types of MAC addresses:

* **Unicast:** Used to identify a single network interface.
* **Multicast:** Used to send data to a specific group of devices.
* **Broadcast:** Used to send data to all devices on the local network.

The broadcast MAC address is:

`FF:FF:FF:FF:FF:FF`

## MAC Address Structure

A standard MAC address contains 48 bits (6 bytes).

The first 24 bits are generally known as the **OUI (Organizationally Unique Identifier)**. They identify the manufacturer or organization that received the address block.

The remaining 24 bits are assigned by the manufacturer to identify the network interface.

**Example:**

`00:1A:2B:3C:4D:5E`

* `00:1A:2B` = OUI (Manufacturer identifier)
* `3C:4D:5E` = Device/interface-specific portion

## MAC Address Lookup

We can know more about the hardware manufacturer by using a MAC Address Lookup tool.

**For that:**

1. Find one MAC address.
2. Copy the MAC address.
3. Go to your browser.
4. Search for **MAC Address Lookup**.
5. Open a MAC lookup website.
6. Paste the MAC address and perform the lookup.

You can usually find:

* Manufacturer / Vendor name
* Organization associated with the OUI
* MAC address registration information

**Note:** MAC lookup does not usually reveal the exact device model, owner, or physical location.

## MAC Spoofing

MAC Spoofing is a technique where someone changes the MAC address of a network interface to another address.

It can be used for:

* Privacy protection
* Testing network security
* Bypassing weak MAC-based filtering
* Authorized security research

However, MAC spoofing does not automatically provide access to a network or bypass strong security controls.

## How to Find MAC Address in Linux (Kali Linux)

We can find the MAC address of our network interfaces using the following commands:

**Command 1:**

```bash
ip link
```

**Command 2:**

```bash
ip addr
```

**Command 3:**

```bash
cat /sys/class/net/eth0/address
```

Replace `eth0` with your actual network interface name.

## Important Things to Remember

* MAC addresses operate at Layer 2 (Data Link Layer).
* A standard MAC address is 48 bits or 12 hexadecimal characters.
* MAC addresses are used for communication within a local network.
* ARP helps map IPv4 addresses to MAC addresses.
* The first 24 bits generally identify the manufacturer (OUI).
* MAC addresses can be spoofed or randomized.
* MAC addresses are not used for routing across the internet; routers use IP addresses for that.

## Practical Learning

Try these activities to understand MAC addresses better:

1. Find your own MAC address using Kali Linux.
2. Identify your network interface name.
3. Perform a MAC Address Lookup.
4. Check your ARP table using:

```bash
ip neigh
```

5. Identify the IP and MAC address mappings in your local network.

**Practice only on your own devices or networks where you have permission.**
