# FTP and TFTP

<!-- nav -->
⬅ [Simple Network Management Protocol (SNMP)](30-simple-network-management-protocol-snmp.md) · [Course index](00_Index.md)
<!-- nav -->

*Network Services · Lesson · Source: https://www.networkacademy.io/ccna/network-services/ftp-and-tftp*

In this lesson, we are going to discuss two very widely adopted protocols called File Transfer Protocol (FTP) and Trivial File Transfer Protocol (TFTP). Both serve the same function-transfer files-but each uses a different network approach, as you will see later on.

## What are FTP and TFTP?

FTP and TFTP are standard protocols for copying files from one host to another. They support all kinds of file types and operate in a client-server model, as shown in the diagram below.

![Client-Server Architecture](../images/network-services/31-ftp-and-tftp--01.svg)

*Figure 1. Client-Server Architecture.*

### What is FTP?

FTP (File Transfer Protocol) is a standard network protocol used to transfer files between a client and a server over the Internet or a local network. It was created in the early days of the Internet and is defined in [RFC 959.](https://www.rfc-editor.org/rfc/rfc959.html)

It uses the TCP transport layer, which means it provides reliable delivery of data. Because it uses TCP, the network stack **ensures that the file is transferred correctly** by checking for errors and resending lost data packets if needed.

![FTP and TFTP and the OSI model](../images/network-services/31-ftp-and-tftp--02.svg)

*Figure 2. FTP and TFTP and the OSI model.*

FTP typically requires authentication (username and password) and operates over TCP. It uses two separate channels: one for commands (control channel) and one for data transfer (data channel) - TCP port 21 for connection control and TCP port 20 for data transfer.

### How does FTP work?

As we have already said, FTP is **a client-server protocol**. This immediately tells you two important things:

- **The client** is the one initiating the connection.
- **The server** is the one that stores the interesting files.

When a client connects to an FTP server, it first establishes a control connection on the well-known TCP port 21. This connection is called **a TCP control connection** and is used to send commands like USER, PASS, LIST, RETR, and STOR, as shown in the diagram below. These commands tell the server what the client wants to do—such as list files, download, or upload.

![FTP Control Connection](../images/network-services/31-ftp-and-tftp--03.svg)

*Figure 3. FTP Control Connection.*

When the actual file transfer begins, **FTP opens a second connection called the data connection**. This is where the file data flows between the two devices. However, there are two FTP modes in the context of opening the data connection —Active Mode and Passive Mode.

#### Active Mode

In Active Mode, when the client wants to transfer data, it informs the server of the random port it has opened for data. Then the server starts the data connection from its port 20 to that client port.

This means **the server initiates the TCP data connection**.

However, if the FTP client is inside a private enterprise network and the FTP server is on the Internet, **active mode fails**. Most firewalls block incoming TCP connections from the Internet unless there is a specific rule allowing them. So what typically happens is that the firewall drops the connection attempt from the server, as shown in the diagram below.

![Active mode issue](../images/network-services/31-ftp-and-tftp--04.svg)

*Figure 4. Active mode issue.*

Active mode works well when **both the FTP client and server are inside the same enterprise network**. In that case, there is usually no NAT or firewall between them.

#### Passive Mode

Passive Mode solves this firewall problem. How? In Passive Mode, the client **initiates both the control and data connections**. This techique makes it work better through firewalls and NAT.

![Passive mode overview](../images/network-services/31-ftp-and-tftp--05.svg)

*Figure 5. Passive mode overview.*

For this reason, Passive mode is most commonly used today even inside the enterprise LAN network, because nowadays security teams filter traffic even inside one organization (zero-trust).

**KEY NOTE:** FTP normally uses two well-known ports—port 21 for control connections and port 20 for data transfers. However, because FTP has evolved over time, it may also **use TCP port 21 for data** connections, as shown in the examples in this lesson.

Now let's switch our focus to TFTP.

### What is TFTP?

**TFTP (Trivial File Transfer Protocol)**is a simpler, less feature-rich protocol compared to FTP. It is designed **for transferring small files between network devices**.

Unlike FTP, **TFTP uses the UDP transport layer** instead of TCP. That means it does not guarantee delivery, and it does not perform error checking or retransmission by itself. It’s faster and smaller but also less reliable.

TFTP uses UDP port 69 for the initial connection. After the session starts, data is transferred using dynamically assigned UDP ports. Because it’s based on UDP and has no authentication, **TFTP is considered insecure**. It’s mainly used in trusted local networks where simplicity is more important than security.

**You might wonder - as a network engineer, why do I need to know how those file transfer protocols work?**

The answer is that, as a network engineer, there are multiple use scenarios when you need to transfer files to a network device, and you need to know how. Additionally, FTP and TFTP are commonly used by all infrastructure teams to transfer files.

![FTP/TFTP file transfer](../images/network-services/31-ftp-and-tftp--06.svg)

*Figure 6. FTP/TFTP file transfer.*

It is very common in Cisco exams, especially at professional and expert levels, to have to transfer a file from one device to another. That's why it is much more valuable to know how to practically copy a file from router R1 to router R2 than to know the super deep details about the FTP and TFTP protocols. So let's make this lesson more Cisco-focused and practical.

## Cisco IOS File System (IFS)

### File Systems

Like other computer systems, Cisco devices use **various types of local storage for files**. Some storage types are **volatile**, meaning they lose their data when the device is powered off, while others are **non-volatile** and retain data even when the device is shut down. **Each storage device is represented as a file system**. The following diagram shows the most common file systems that a Cisco device has:

- **RAM:** Volatile memory for the running configuration and the running operating system image (IOS). Represented by the prefix **system:**.
- **NVRAM:** Non-volatile memory that stores the startup configuration file. Represented by the prefix **nvram:**.
- **Flash Memory:** Non-volatile memory that stores IOS images, configuration backups, debug files, and so on. Typically represented by the prefixes **flash:**, **bootflash:**or **disk:**.
- **ROM:** Read-only non-volatile memory used for system bootstrap processes.
- **USB Drives:** Some devices support external USB storage for data transfers and backups. Represented as usbflash0: or similar.

![Cisco IOS File System (IFS)](../images/network-services/31-ftp-and-tftp--07.svg)

*Figure 7. Cisco IOS File System (IFS).*

Each file system has a prefix that is used when working with that storage. For example, you can access a file stored in the device's NVRAM using the prefix **nvram:** and the filename via the CLI like this **nvram:**<filename>.

Additionally, every device can access remote file systems using various transport protocols such as FTP, TFTP, HTTP, SCP, etc. Each file transfer protocol is represented by a prefix in the CLI. For example, you can access a file on a remote FTP server using the CLI command **ftp:**<user:pass>@<server-IP>/<filename>.

We check the filesystem (IFS) on a Cisco device using the following command:

```text
R1# show file systems

File Systems:
       Size(b)       Free(b)      Type  Flags  Prefixes
        524288        514208     nvram     rw   nvram:
             -             -    opaque     rw   system:
             -             -    opaque     rw   tmpsys:
*   2147479552    2147479552      disk     rw   flash:
             -             -    opaque     rw   null:
             -             -    opaque     ro   tar:
             -             -   network     rw   tftp:
             -             -    opaque     wo   syslog:
             -             -   network     rw   rcp:
             -             -   network     rw   ftp:
             -             -   network     rw   http:
             -             -   network     rw   scp:
             -             -   network     rw   sftp:
             -             -   network     rw   https:
             -             -    opaque     ro   cns:
```

Notice that each file system has a type that indicates what kind of storage device it is. There are four general types, highlighted in different colors.

- ****opaque**** - It means this storage is used for various internal functions. For example, the show run command internally links to the system:running-config file.
- ****network**** - This file type provides access to external file systems like TFTP, FTP, HTTP, or SCP servers. We can use this to copy files from these external sources to our filesystem.
- ****disk**** - This is used for storage devices such as flash memory or USB sticks.
- ****nvram**** - This refers to the internal NVRAM where the startup-config file is stored.

The flags are pretty self-explanatory. They indicate the permissions for the filesystem:

- **ro:** read-only
- **rw:** read and write
- **wo:** write-only

### Directory Structure

Each file system has a directory structure that organizes files and subdirectories. It has the following format: prefix:/directory/filename. For example, an IOS stored in Flash has the following directory structure: **flash:**/directory/filename.

---

<!-- nav -->
⬅ [Simple Network Management Protocol (SNMP)](30-simple-network-management-protocol-snmp.md) · [Course index](00_Index.md)
<!-- nav -->
