# Load Balancers

<!-- nav -->
⬅ [Firewalls](14-firewalls.md) · [Course index](00_Index.md) · [Proxy Servers](16-proxy-servers.md) ➡
<!-- nav -->

*Network Fundamentals · Lesson · Source: https://www.networkacademy.io/ccna/network-fundamentals/load-balancer*

In this lesson, we will quickly discuss a common network devices that operate at Layer 7 of the OSI model, called **a Load Balancer**. Although it is not part of the CCNA blueprint as of the latest version, the load balancer typically falls under the responsibility of the organization's network team. It is an excellent foundation for a network engineer to be aware that they can encounter such a device in a real enterprise network.

In modern infrastructures, application performance and scalability are very important. Standard network devices like switches and routers move traffic, but they do not keep track of an application's performance. This is where specialized network devices come in.

## Why do we need a Load Balancer?

To understand why we need specialized network devices such as the load balancer, let's walk through the following example. Imagine that a company has an e-commerce web application (online store). The web address of the store is www.xyz.com.

Now, imagine that the web app runs on a single, very large and powerful server, as shown in the diagram below.

![Why do we need a network load balancer?](../images/network-fundamentals/15-load-balancer--01.svg)

*Figure 1. Why do we need a network load balancer?*

It is evident that this design has several significant drawbacks - **it is not highly available and lacks scalability**. For example, **if the server encounters a hardware problem** and goes down, the online store goes offline, and the company loses money (which is always a bad thing).

Additionally, even if the server is perfectly healthy, **it will eventually get overloaded**. It has limited CPU, RAM, and network capacity. When **too many users connect at the same time**, it will become slow or unresponsive. So what do you think is the solution to this infrastructure problem?

The first thing that comes to mind is to run the web application on multiple servers. That way, it will be able to handle many more users. **But there’s a problem**:

- Users access the online store via its domain name xyz.com. Before a user opens the web app, their PC first **resolves the domain name to an IP address** using DNS.
- However, DNS can only resolve a domain name **to a single IP address**. The URL xyz.com resolves to 37.3.2.1.

So if you have 100 servers, **where do you place the IP address 37.3.2.1** that the store's domain name resolves to? If you put it on any of the servers, all users would still go to just one server.

A load balancer is a network device that is designed to solve this problem, as shown in the diagram below.

![What is a network load balancer?](../images/network-fundamentals/15-load-balancer--02.svg)

*Figure 2. What is a network load balancer?*

The solution is to place the e-commerce web app's IP address on the load balancer. **DNS points to the load balancer’s IP**. All user HTTPS connections terminate at the load balancer. It then forwards each incoming connection to one of the backend servers. This **spreads the traffic across all servers**, preventing any single server from getting overloaded.

Notice the thicker green line from the Internet to the Load Balancer. This represents thousands of incoming connections. The LB spreads those thousand connections to multiple servers. So the number of incoming requests to each individual server is way lower (hence the thinner green line to each server).

## How does the load balancer work?

A load balancer’s main job is **to distribute incoming connections across a group of servers**. Because most traffic today is TLS-encrypted, the load balancer first **handles HTTPS decryption** by presenting the site’s SSL certificate to clients. After that, it selects a backend server using a scheduling method such as Round Robin or Least Connections. The load balancer can then forward the request to the chosen server over plain HTTP, which reduces the CPU load on the servers by offloading the encryption work.

However, nowadays, a load balancer does many more functions than just spreading traffic across servers and performing TLS termination. The most notable ones are as follows:

- **Health checking:** It monitors the status of servers and only sends traffic to healthy ones. If a server goes down, the load balancer automatically removes it from rotation, as shown in the diagram below.

![Load Balancer High Availability](../images/network-fundamentals/15-load-balancer--03.svg)

*Figure 3. Load Balancer High Availability.*

- **Failover:** If one or more servers have to be **taken offline for maintenance**, it can redirect traffic to backup servers or even another data center.
- **Traffic shaping and routing:** It can direct requests based on rules, like sending certain types of traffic **to the nearest geographic location**.
- **Security functions:** It can **block suspicious traffic** and hide backend servers from the public network.
- **Horizontal Scalability:** A load balancer makes it possible **to add or remove servers without disrupting users**. This is one of the most significant advantages of the load balancer.

So while its basic job is spreading connections, a load balancer also **improves the availability, performance, security, and flexibility** of the app infrastructure.

## Popular Load Balancers

Now, let's quickly introduce the most popular load balancer vendors you may encounter during your networking career.

### Hardware Load Balancers

In the early days, load balancers were hardware, tangible devices installed in a rack cabinet somewhere in the data center. Nowadays, this is not the most common case, but still, many hardware appliances are operational.

The most popular and widespread vendor of hardware load balancers is F5. F5 appliances have been widely used in data centers for many years to handle large volumes of traffic and provide advanced features like SSL offloading, application firewall, and traffic shaping.

![Popular Hardware Load Balancers](../images/network-fundamentals/15-load-balancer--04.png)

*Figure 4. Popular Hardware Load Balancers.*

Other known brands include Citrix (NetScaler) and A10 Networks, but F5 is generally the most well-known and widely deployed.

### Virtual Load Balancers

Most modern load balancers are no longer physical hardware devices. In the past, companies used dedicated load balancer appliances — physical boxes placed in data centers. However, the problem with hardware boxes is that **they have a fixed capacity** and need manual setup and maintenance.

Today, **most load balancers are virtual**. They run as software in the cloud or on virtual machines. For example, AWS Elastic Load Balancer (ELB) is not a physical device — it’s a managed service. You don’t see or touch the hardware. AWS automatically creates and scales it in the background.

![AWS Elastic Load Balancer](../images/network-fundamentals/15-load-balancer--05.svg)

*Figure 5. AWS Elastic Load Balancer.*

This virtual approach is more flexible, easier to scale, and cheaper to manage than buying and maintaining physical load balancers.

## Key Takeaways

- Load balancers distribute traffic across multiple servers. They prevent overload and ensure high availability.
- They offload TLS decryption from servers.
- They perform health checks and route traffic only to healthy servers.
- They support failover and traffic shaping.
- They improve scalability, performance, and security.
- Popular vendors include F5, Citrix, A10, and AWS.

---

<!-- nav -->
⬅ [Firewalls](14-firewalls.md) · [Course index](00_Index.md) · [Proxy Servers](16-proxy-servers.md) ➡
<!-- nav -->
