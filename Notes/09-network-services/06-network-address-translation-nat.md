# Network Address Translation (NAT)

<!-- nav -->
⬅ [Cisco Discovery Protocol (CDP)](05-cisco-discovery-protocol-cdp.md) · [Course index](00_Index.md) · [Why do we need NAT?](07-why-do-we-need-nat.md) ➡
<!-- nav -->

*Network Services · Section overview · Source: https://www.networkacademy.io/ccna/network-services/network-address-translation-nat*

In this section of the CCNA Network Services course, we will explore Network Address Translation (NAT), a critical service in modern networks that allows devices in private networks to communicate with the public Internet. NAT plays an essential role in IP address management and security and enables smooth internal and external network operations. By the end of this section, you will have a comprehensive understanding of NAT, its types, practical applications, and troubleshooting techniques.

**Lesson 1: Why Do We Need NAT?**

In the early days of networking, the expectation was that every device would have a unique public IPv4 address. However, the explosive growth of devices connected to the internet caused IPv4 address depletion. NAT was introduced to address this issue by allowing multiple devices on a private network to share a single public IP address, enabling seamless access to the internet without requiring every device to have a unique public IP.

Key reasons we need NAT:

- **IPv4 Address Conservation:** NAT reduces the demand for public IPv4 addresses.
- **Security**: NAT hides internal IP addresses, offering a layer of protection by preventing direct access from external networks.
- **IP Address Reuse:** Private IP ranges (defined in RFC 1918) can be reused within different networks without causing conflicts.

**Lesson 2: Static NAT**

Static NAT maps a single private IP address to a single public IP address. This is a one-to-one mapping, meaning that a specific device on the internal network is always reachable from the outside using a consistent public IP address. Static NAT is commonly used for:

- Servers or devices that need to be accessible from the public internet, such as web or mail servers.
- Increased security by exposing only specific devices while the rest of the network remains hidden.

Key Characteristics:

- **One-to-one mapping**: Fixed correspondence between private and public IP addresses.
- Suitable for services that must be reachable from the internet (e.g., a web server).

**Lesson 3: Dynamic NAT**

Dynamic NAT provides a temporary one-to-one mapping between private IP addresses and a pool of public IP addresses. Unlike Static NAT, where the mapping is fixed, Dynamic NAT assigns public IP addresses from a pool dynamically when internal devices initiate traffic to the internet. Once the session ends, the public IP becomes available for use by other devices.

This type of NAT is used when:

- You have more devices on the internal network than available public IP addresses.
- The internal devices do not need a permanent public address.

Key Characteristics:

- **Many-to-many mapping**: Private addresses are mapped to a pool of public addresses dynamically.
- Public IPs are assigned only when needed, and the mappings are temporary.

**Lesson 4: Port Address Translation (PAT) or NAT Overload**

Port Address Translation (PAT), also known as NAT Overload, is the most common type of NAT used in home and office networks. It allows multiple devices to share a single public IP address by differentiating traffic using TCP or UDP port numbers. This allows hundreds or thousands of devices to connect to the internet simultaneously using only one public IP address.

PAT is essential for environments where:

- You have limited public IP addresses.
- Many devices need internet access simultaneously.

Key Characteristics:

- **Many-to-one mapping**: Multiple private IP addresses are mapped to a single public IP, with each session differentiated by port numbers.
- Efficient use of a single public IP for multiple devices.
- Used extensively in home and small office networks.

**Lesson 5: NAT Troubleshooting**

Proper configuration of NAT is critical for ensuring smooth network operations. Common issues include misconfigurations in NAT rules, missing address translations, or improper IP pool management. Troubleshooting NAT involves:

- **Verifying NAT Translations**: Use commands like show ip nat translations to check if translations are happening as expected.
- **Inspecting ACLs**: Ensure that Access Control Lists (ACLs) correctly permit traffic for NAT.
- **Overlapping Subnets**: Verify that internal and external IP subnets don’t overlap.
- **Check Overload (PAT) Usage**: Ensure that port overloading is configured correctly when using PAT.

**Lesson 6: Lab Example #1 – Enabling Internet Access for a Small Office**

In this lab, we will configure NAT Overload (PAT) to enable a small office network to access the internet using a single public IP address.

**Lesson 7: Lab Example #2 – Connecting a Corporate Web Server to the Internet**

In this lab, we will configure Static NAT to allow a corporate web server to be accessible from the internet.

By completing this section, you'll gain the skills necessary to implement and troubleshoot NAT in both small office and enterprise network environments. NAT is a crucial part of the CCNA certification and a foundational skill for network professionals.

---

<!-- nav -->
⬅ [Cisco Discovery Protocol (CDP)](05-cisco-discovery-protocol-cdp.md) · [Course index](00_Index.md) · [Why do we need NAT?](07-why-do-we-need-nat.md) ➡
<!-- nav -->
