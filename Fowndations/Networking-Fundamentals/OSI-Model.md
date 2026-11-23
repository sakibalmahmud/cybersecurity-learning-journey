# OSI Model

The **OSI (Open Systems Interconnection)** Model is a networking framework that defines how different computer systems communicate over a network.

It was developed by the **International Organization for Standardization (ISO)** in the late 1970s and standardized in 1984.

★ It divides the networking process into **7 layers**. Each layer has its own specific responsibilities.

## The 7 Layers of the OSI Model

### 7. Application Layer

* Closest to the user.
* Provides network services and interfaces to applications.
* Allows applications to communicate over a network.

**Examples:** HTTP, HTTPS, FTP, DNS, SMTP, POP3, IMAP.

### 6. Presentation Layer

* Translates data into a format understandable by the application.
* Handles data encryption, decryption, compression, and encoding.
* Ensures that data is presented in a usable format.

**Examples:** JPEG, PNG, MPEG, Unicode, MIME, TLS.

### 5. Session Layer

* Handles opening, maintaining, and closing communication sessions.
* Manages communication between two devices.
* Helps synchronize data exchange.

**Examples:** RPC, NetBIOS, NFS.

### 4. Transport Layer

* Ensures end-to-end data delivery between devices.
* Breaks data into smaller segments.
* Handles flow control and error recovery when supported by the protocol.

**Examples:** TCP, UDP.

### 3. Network Layer

* Responsible for routing data across different networks.
* Uses IP addresses to identify source and destination devices.
* Determines the path that data should take.

**Examples:** IP, ICMP, IPsec.

**Device:** Router.

### 2. Data Link Layer

* Responsible for transferring data between directly connected devices.
* Uses MAC addresses for local network communication.
* Organizes data into frames.
* Ethernet and Wi-Fi provide data-link functionality.

**Examples:** Ethernet (IEEE 802.3), Wi-Fi (IEEE 802.11).

**Device:** Switch.

### 1. Physical Layer

* Responsible for the physical transmission of data.
* Transmits raw bits (0s and 1s) through physical or wireless media.
* Defines electrical, optical, and radio signal characteristics.

**Examples:** Ethernet cables, fiber-optic cables, radio signals, Wi-Fi signals.

**Device:** Hub, repeater.

---

## How the OSI Model Works

When you send data from one computer to another, it passes through the OSI layers.

**Sending Process (Encapsulation):**

1. Application Layer — Creates the data.
2. Presentation Layer — Formats, encrypts, or compresses the data.
3. Session Layer — Manages the communication session.
4. Transport Layer — Divides data into segments.
5. Network Layer — Adds logical IP addressing and handles routing.
6. Data Link Layer — Creates frames and adds MAC addressing.
7. Physical Layer — Transmits bits through the network medium.

**Receiving Process (Decapsulation):**

When the receiving device gets the data, it moves upward from Layer 1 to Layer 7. Each layer processes and removes the information added by its corresponding layer.

This process allows two devices to communicate successfully.

## PDU (Protocol Data Unit)

Each layer uses a different name for the data it handles.

| OSI Layer                          | PDU Name                       |
| ---------------------------------- | ------------------------------ |
| Application, Presentation, Session | Data                           |
| Transport                          | Segment (TCP) / Datagram (UDP) |
| Network                            | Packet                         |
| Data Link                          | Frame                          |
| Physical                           | Bits                           |

---

# TCP/IP Model

The **TCP/IP Model** is a networking model used for communication over the internet.

Unlike the OSI Model, which has 7 layers, the commonly used TCP/IP Model has **4 layers**.

It combines some of the OSI Model's layers into broader categories.

## TCP/IP Model Layers

### 4. Application Layer

* Provides network services to applications.
* Combines the Application, Presentation, and Session layers of the OSI Model.

**Examples:** HTTP, HTTPS, FTP, DNS, SMTP, IMAP, POP3.

### 3. Transport Layer

* Provides communication between applications on different devices.
* Handles data segmentation and transport.
* Uses TCP or UDP.

**Examples:** TCP, UDP.

### 2. Internet Layer

* Handles logical addressing and routing between networks.
* Uses IP addresses to deliver packets.

**Examples:** IPv4, IPv6, ICMP.

### 1. Network Access Layer

* Handles communication over the local network.
* Responsible for framing and physical transmission.
* Combines the Data Link and Physical layers of the OSI Model.

**Examples:** Ethernet, Wi-Fi.

---

## OSI Model vs TCP/IP Model

| OSI Model       | TCP/IP Model      |
| --------------- | ----------------- |
| 7. Application  | 4. Application    |
| 6. Presentation | 4. Application    |
| 5. Session      | 4. Application    |
| 4. Transport    | 3. Transport      |
| 3. Network      | 2. Internet       |
| 2. Data Link    | 1. Network Access |
| 1. Physical     | 1. Network Access |

## Comparison Between OSI and TCP/IP

| Feature          | OSI Model                       | TCP/IP Model                                     |
| ---------------- | ------------------------------- | ------------------------------------------------ |
| Number of Layers | 7 Layers                        | 4 Layers                                         |
| Developed By     | ISO                             | DARPA / DoD                                      |
| Main Purpose     | Conceptual networking framework | Practical communication model                    |
| Usage            | Learning and troubleshooting    | Real-world networking and internet communication |
| Structure        | More detailed                   | More simplified                                  |

---

## Important Things to Remember

* OSI Model has 7 layers.
* TCP/IP Model commonly has 4 layers.
* Application Layer is the closest to the user.
* Physical Layer handles the transmission of raw bits.
* Transport Layer uses TCP and UDP.
* Network Layer uses IP addresses.
* Data Link Layer uses MAC addresses.
* Routers primarily operate at Layer 3.
* Switches primarily operate at Layer 2.
* Encapsulation happens when data moves down the layers.
* Decapsulation happens when data moves up the layers.

## Practical Learning

Try these activities to understand the OSI Model better:

1. Identify the 7 layers of the OSI Model.
2. Understand the difference between IP addresses and MAC addresses.
3. Learn how TCP and UDP work at the Transport Layer.
4. Use Wireshark to capture network packets.
5. Identify Ethernet, IP, TCP, and HTTP information inside captured packets.
6. Practice troubleshooting network problems by thinking about the different OSI layers.

**Practice only on your own devices, authorized networks, or TryHackMe labs.**
