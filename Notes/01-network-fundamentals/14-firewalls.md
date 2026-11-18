# Firewalls

<!-- nav -->
⬅ [Routers and L3 Switches](13-routers-layer3-switches.md) · [Course index](00_Index.md) · [Load Balancers](15-load-balancer.md) ➡
<!-- nav -->

*Network Fundamentals · Lesson · Source: https://www.networkacademy.io/ccna/network-fundamentals/firewalls*

In this lesson, we examine the network firewall - a security device that operates **at Layer 4 of the OSI model** and guards the perimeter of the network. The following diagram shows the most common icons used to visualize a Cisco firewall in the network topology.

![Cisco Firewall icons](../images/network-fundamentals/14-firewalls--01.svg)

*Figure 1. Cisco Firewall icons.*

## Why do we need a firewall?

The Internet **is not a friendly place**. Every device connected to it is exposed **to millions of unknown systems and users**. Some of these are harmless, but many can try to steal data, disrupt services, or take control of the organization's internal systems. Nowadays, with the rise of AI, Internet threats have become more sophisticated than ever.

The following diagram shows a small internal network connected directly to the Internet **without any protection**. Switches and routers are designed to move network traffic, not to stop attacks. Anyone from the outside can access internal resources and attempt to steal sensitive data or disrupt essential services.

![Why do we need a firewall?](../images/network-fundamentals/14-firewalls--02.svg)

*Figure 2. Why do we need a firewall?*

A firewall acts as the first line of defense, most commonly at the perimeter of the network. It helps ensure that **only trusted traffic is allowed**, and suspicious or dangerous traffic is blocked before it reaches the internal network.

The most common function of the firewall is to block unwanted traffic from the outside from accessing resources on the internal network, as shown in the diagram below.

![Firewall blocks unwanted traffic.](../images/network-fundamentals/14-firewalls--03.svg)

*Figure 3. Firewall blocks unwanted traffic.*

It checks network packets against the configured security rules to determine whether each packet should pass or be blocked. This helps make sure only safe and trusted traffic goes through.

## How does a firewall work?

A firewall works at Layer 4 of the OSI model. This means it reads the headers from Layer 2, Layer 3, and Layer 4, as shown in yellow in the diagram below. It has all the information at its disposal, such as MAC addresses, IP addresses, and port numbers, and the transport protocol used (TCP or UDP).

![How does a firewall work.](../images/network-fundamentals/14-firewalls--04.svg)

*Figure 4. How does a firewall work.*

With this information, the firewall makes the so-called ****"6-tuple"**** - a set of six key values from a packet’s headers that a firewall can use to uniquely identify a specific network flow. For example:

```text
(Source IP,   Destination IP, Source Port, Destination Port, Protocol, Direction)
(192.168.1.10,  23.0.13.20,   51514,       443,               TCP,      Outbound)
```

This six-tuple combination **uniquely identifies the following flow**: traffic from source IP 192.168.1.10, source port 51514, going to destination IP 23.0.13.20, destination port 443, using the TCP protocol, in the outbound direction. A security administrator can configure the firewall to allow or drop this traffic flow.

### Inside and Outside zones

Another essential aspect is that a firewall works by separating the network into an inside (trusted) and outside (untrusted) zone, as shown in the diagram below:

- ****The inside**** is the trusted side. This is usually the organization's internal network, where company computers, servers, and internal resources live. Traffic on the inside is assumed to be safe, and the firewall’s job is to protect it from dangerous access.
- ****The outside**** is the untrusted side. This typically refers to the Internet or any network that the organization doesn’t control. Traffic from this side can be risky because it comes from potentially malicious sources.

![Firewall zones](../images/network-fundamentals/14-firewalls--05.svg)

*Figure 5. Firewall zones.*

Many firewalls, especially in Cisco networks, use a security-level value to define how trusted an interface is. Security levels range from 0 to 100:

- **Inside**interfaces are usually set to 100 (most trusted).
- **Outside**interfaces are usually set to 0 (least trusted).
- Any other network, like a **DMZ**, might be set somewhere in between (e.g., 50).

By default, **traffic is allowed to flow from higher security levels to lower ones** (inside to outside) but is blocked in the opposite direction (outside to inside) unless specific rules permit it. This concept makes the firewall secure the network perimeter **out of the box**. Even if the security team hasn’t written a single firewall rule, the device is already protecting the network, because:

- **Internal users** can reach the Internet because outbound traffic is allowed (the green arrow in the diagram above).
- **External users** cannot reach the internal network because inbound traffic is denied (the red arrows in the diagram above).

This “out of the box” protection ensures the network perimeter is secure from unsolicited inbound connections immediately after setting interface security levels.

### Stateful inspection

The firewall zoning with security levels is combined with another technique called **stateful inspection**. It means the firewall doesn’t just look at each packet in isolation — i**t tracks the state of active connections**.

- When a new connection is initiated (for example, a user opens a website), the firewall allows it because it comes from a higher security level (100) to a lower security level (0).
- When the traffic goes out, the firewall creates an entry in a state table with details like source/destination IP, ports, and protocol.
- Return traffic that matches this entry is automatically allowed, even if there’s no explicit rule for it.

![Stateful Firewall](../images/network-fundamentals/14-firewalls--06.svg)

*Figure 6. Stateful Firewall.*

When the connection ends or times out, the entry is removed, and any further packets are blocked unless a new session is allowed. Why it’s important:

- Blocks unsolicited traffic while letting replies through.
- More secure and efficient than just filtering by static rules.
- Supports protocols that open temporary ports (e.g., FTP, VoIP).

If you want, I can show you a simple diagram of a state table and how packets flow through it.

## Firewall use-cases

Lastly, let's discuss the design side of things. The most common place to deploy a firewall is **at the network perimeter**—between the organization’s internal network (trusted) and the internet (untrusted). This allows it to filter inbound and outbound traffic, blocking threats before they reach internal network.

![Firewall placement](../images/network-fundamentals/14-firewalls--07.svg)

*Figure 7. Firewall placement.*

Most organizations also use internal firewalls **to segment the network**. For example, an organization places a firewall between user networks and sensitive departments like finance or R&D. This limits the damage if an attacker gets inside and helps enforce access controls between teams.

## Key Takeaways

- A firewall is **a Layer 4 security device** that protects the network perimeter by filtering traffic based on IP addresses, ports, and protocols.
- It separates the network into zones, usually ****inside (trusted)**** and ****outside (untrusted)****, and can also include intermediate zones like a DMZ.
- Cisco firewalls use **security levels (0–100) to define trust**.
  - By default, traffic is allowed from higher to lower levels, but blocked in the opposite direction.
  - This provides out-of-the-box protection even without custom rules.
- **Stateful inspection** lets the firewall track active connections, automatically allowing return traffic while blocking unsolicited packets.
- Firewalls can be placed **at the perimeter** to filter Internet traffic or **inside**the network to segment and protect sensitive areas.

---

<!-- nav -->
⬅ [Routers and L3 Switches](13-routers-layer3-switches.md) · [Course index](00_Index.md) · [Load Balancers](15-load-balancer.md) ➡
<!-- nav -->
