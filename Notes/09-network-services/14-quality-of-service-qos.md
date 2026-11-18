# Quality of Service (QoS)

<!-- nav -->
⬅ [Lab #2.2 - Overlapping IP ranges](13-lab-2-overlapping-ip-ranges.md) · [Course index](00_Index.md) · [Why do we need QoS?](15-why-do-we-need-qos.md) ➡
<!-- nav -->

*Network Services · Section overview · Source: https://www.networkacademy.io/ccna/network-services/quality-of-service-qos*

In modern networks, a wide range of applications with diverse needs—such as voice, video, and data—are transmitted across the same network infrastructure. QoS techniques allow network administrators to manage bandwidth, reduce latency, and prioritize certain types of traffic to ensure that critical applications perform optimally, even when the network is under heavy load.

In this section, you'll learn the fundamental concepts and practical applications of QoS, preparing you to implement QoS policies that improve network performance and meet application requirements. By the end, you'll understand how to use QoS tools to classify, prioritize, and manage network traffic effectively.

## Lessons Overview

**Lesson 1: Why do we need QoS in Networking?**

This introductory lesson explores the need for QoS in today’s networks. We'll examine the challenges of transmitting diverse traffic types across shared resources, such as bandwidth limitations, latency, jitter, and packet loss. You’ll understand why QoS is critical for ensuring the smooth functioning of time-sensitive applications like VoIP and video streaming.

**Lesson 2: Classification and Marking**

In this lesson, we delve into the basics of traffic classification and marking, the foundational steps for QoS. You'll learn how to identify different types of traffic and mark packets for prioritization. Classification and marking are essential to telling the network how to handle each packet, setting the stage for effective QoS policies.

**Lesson 3: Queuing and Scheduling**

Queuing and scheduling are at the heart of QoS, determining how packets are managed when congestion occurs. This lesson covers various queuing methods, such as FIFO, priority queuing, and weighted fair queuing (WFQ). You’ll learn how to schedule packets to ensure that high-priority traffic receives the necessary resources.

**Lesson 4: Policing**

Policing controls the rate of traffic allowed into the network by discarding or marking packets that exceed predefined thresholds. This lesson explains how to enforce traffic limits to maintain network stability and prevent any single application from consuming excessive bandwidth.

**Lesson 5: Shaping**

Shaping is a traffic management technique that smooths out traffic flow, delaying packets as needed to ensure compliance with bandwidth limits. In this lesson, you’ll explore how shaping differs from policing and how it can help manage bursts of traffic without dropping packets.

**Lesson 6: Congestion Avoidance**

Congestion avoidance is a proactive QoS technique that prevents network congestion before it becomes critical. This lesson introduces mechanisms like Weighted Random Early Detection (WRED), which selectively drops packets to avoid buffer overflow and maintain optimal performance.

**Lesson 7: LAB 1 - Basic QoS Configuration**

In this hands-on lab, you’ll apply the concepts covered in the previous lessons by configuring basic QoS settings on network devices. This practical exercise solidifies your understanding of QoS principles and prepares you to implement QoS in real-world scenarios.

By the end of this section, you’ll have a solid foundation in Quality of Service and the skills to implement QoS policies that enhance network reliability and performance. Dive in and discover how QoS can transform network efficiency and user experience!

---

<!-- nav -->
⬅ [Lab #2.2 - Overlapping IP ranges](13-lab-2-overlapping-ip-ranges.md) · [Course index](00_Index.md) · [Why do we need QoS?](15-why-do-we-need-qos.md) ➡
<!-- nav -->
