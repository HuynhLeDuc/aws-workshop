---
title: "Blog 2"

weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Modernizing trading workloads with next-generation AWS Outposts racks

<span style="font-size:13px; color: #737070ff;">
by Jim Cotis | on 01 MAY 2025 | in
</span>
<small

<a href="https://aws.amazon.com/blogs/industries/category/compute/amazon-ec2/" style="color:#0073bb; text-decoration:none;">Amazon EC2</a>, 
<a href="https://aws.amazon.com/blogs/industries/category/compute/amazon-kubernetes-service/" style="color:#0073bb; text-decoration:none;">Amazon Elastic Kubernetes Service</a>, 
<a href="https://aws.amazon.com/blogs/industries/category/compute/amazon-vpc/" style="color:#0073bb; text-decoration:none;">Amazon VPC</a>, 
<a href="https://aws.amazon.com/blogs/industries/category/compute/aws-outposts/" style="color:#0073bb; text-decoration:none;">AWS Outposts</a>, 
<a href="https://aws.amazon.com/blogs/industries/category/industries/financial-services/" style="color:#0073bb; text-decoration:none;">Financial Services</a> 
 <a href="https://aws.amazon.com/blogs/industries/category/industries/" style="color:#0073bb; text-decoration:none;">Industries Permalink  Comments </a>
</small>


## Introduction
In today’s fast-paced world of financial technology, sub-milliseconds can make the difference between success and failure in financial transactions. The demands of high-frequency trading, real-time market data processing, and complex financial transactions require an infrastructure that will deliver unparalleled performance, reliability, and fairness. AWS is addressing these needs through a new category of Amazon Elastic Compute Cloud (Amazon EC2) instances featuring accelerated networking on second-generation AWS Outposts racks. These include Bmn-sf2e instances for ultra-low latency and deterministic performance, and Bmn-cx2 instances for high throughput and low latency.

Outposts racks with accelerated networking EC2 instances include bare metal instances, accelerated networking, native L2/L3 multicast capabilities, Precision Time Protocol (PTP) support, and equal length cabling, all designed to address the unique challenges faced by market participants, exchanges, and trading venues. Our solutions not only meet the stringent performance requirements of modern financial markets but also adhere to global regulatory standards, facilitating fair access to every participant.

At the heart of our offering is the concept of static stability, a principle that enables continuous operation even in the face of component failures or regional disruptions. This approach, combined with our cutting-edge technologies, provides a robust foundation for the most demanding financial applications.


>Nasdaq has successfully migrated the core trading system of three North American markets to a cloud-enabled market infrastructure using AWS Outposts with accelerated networking Amazon EC2 instances, with the largest market processing up to 36 billion in daily messaging. The cloud-enabled market infrastructure delivered a low double-digit microsecond latency for end-to-end and order-to-trade processes, along with up to 10% performance improvement in round-trip latency. Building on the success of modernizing Nasdaq’s markets, Nasdaq and AWS are excited to make this innovation available to global capital markets as part of the recently announced modernization blueprint. – Nasdaq

Let’s explore these components to understand how they come together to deliver a performant, compliant, and resilient infrastructure for trading, post-trade, and real-time market data distribution and consumption workloads.

## Features of accelerated networking EC2 instances

#### Bare metal compute
Financial transactions demand minimal latency and jitter. These accelerated networking EC2 instances are available as bare metal compute instances, directly addressing these performance requirements. These instances operate without virtualization, helping developers to control CPU affinity for their applications. This control allows Non-Uniform Memory Access (NUMA) optimization, which reduces memory access time and enhances overall performance.

#### Accelerated networking
Financial markets depend on high-performance networks that enable asset-to-cash conversions. These private networks must ensure equal access and fairness for all participants while maintaining minimal latency. Our new bare metal networking architecture addresses these requirements with specialized network interface cards (NICs) directly connected to top-of-rack switches. They are a secondary physical network independent of the Amazon Virtual Private Cloud (VPC) in each Outpost. This design allows direct participation in private financial networks, delivering the performance these markets demand.

#### Native L2/L3 multicast
Exchanges and trading venues use IP multicast to broadcast real-time market data (quotes, trades, order book updates) to thousands of subscribers simultaneously. By taking advantage of the underlying network fabric, these venues can eliminate the overhead of establishing individual connections to each market participant as well as conform to fair and equal access market requirements. Our bare metal network includes a dedicated switch fabric with layer 2 and layer 3 (L2/L3) multicast capabilities. The network maintains zero oversubscription across all physical paths, ensuring consistent performance for every participant.

#### Precision Time Protocol (PTP)
Precision Time Protocol (PTP) synchronizes trading systems to nanosecond accuracy, enabling precise sequencing of orders in a trading system. This level of synchronization is crucial for maintaining accurate order priority in fast-moving markets and prevent disputes over which orders arrived first.

#### Equal length cabling
Financial markets worldwide are governed by regulations that require fair access for all participants. In the United States, Regulation NMS (National Market System) mandates exchanges to provide non-discriminatory access. Similarly, in Europe, the Markets in Financial Instruments Directive II (MiFID II) enforce fair and equal access to trading venues. These regulations reflect a global trend among major jurisdictions to maintain equitable market conditions. To comply with these fairness requirements, our solution uses Amazon EC2 instances connected to financial networks via equal length cabling. This approach ensures all participants have uniform access to the matching engines hosted on EC2, thereby supporting regulatory compliance and market integrity.

The following is an image of AWS Outpost Rack with accelerated networking. The fiber cables in blue are all of equal length, connecting them to the Top of Rack (TOR) switches above.


![Translate blog 2](/images/3-BlogsTranslated/3.2-Blog2/k1.png)
>*Figure 1: Photo of an AWS Outposts rack with accelerated networking*

 

LSEG Markets will use AWS Outposts as part of its strategy within its FX business to deliver low latency trading solutions, which are resilient and scalable. These solutions use core AWS services to bring innovative new features to market. – LSEG

## Solution

![Translate blog 2](/images/3-BlogsTranslated/3.2-Blog2/k2.png)

> *Figure 2 – Architecture of common AWS Outposts deployment patterns*

The illustration above depicts common AWS Outposts deployment patterns observed across financial services customers. It showcases three Outposts configurations, each represented distinctly. Two of these Outposts use Amazon Elastic Kubernetes Service (EKS). The control plane extends from the AWS Region while worker nodes operate locally on the Outposts. The third Outpost, shown at the bottom of the illustration, leverages only accelerated networking EC2 instances.

This configuration can deliver ultra-low latency computing, maintain regulatory compliance through on-premises data processing, and provide a consistent hybrid experience. The diagram exhibits the performance optimization possibilities, the enhanced security features via the Nitro system, and the flexibility offered through the combination of containerized workloads and bare metal EC2 instances. AWS Outposts can provide a comprehensive infrastructure solution tailored to the unique demands of the financial services sector.

## Benefits
#### Proximity to liquidity
Capital market firms seek proximity to financial exchanges and liquidity providers to gain competitive advantages. This closeness reduces latency when receiving market data and executing orders, which firms use to react swiftly to market changes. AWS Outposts enables participants to position their cloud solutions near these critical financial hubs. Our bare metal network (BMN) instances can directly connect to exchange co-location facilities, integrating with existing financial infrastructure. This combination of proximity and direct connectivity maximizes speed and efficiency for market participants.

#### Static stability
AWS defines static stability as a fundamental operational principle where systems design includes the ability to continue functioning correctly even when components fail, without requiring immediate human intervention or automated recovery actions. AWS Outposts racks with accelerated networking EC2 instances incorporate static stability as a key component. By minimizing all AWS Region dependencies and only offering instance storage, with local boot, we ensure that any disruption to a service running in our Region has no impact on the operation of any application running on the accelerated networking EC2 instances. In collaboration with our customers, we’ve successfully tested these instances operating for over a week when temporarily disconnected from the Region, with well architected applications.

#### AWS Console and API command and control
Core design principles form the foundation of modern cloud services, emphasizing consistency across all service interactions and a robust Service-Oriented Architecture (SOA). These services, built with an API-first mindset, ensure that every feature is accessible programmatically before being implemented in user interfaces. Security is part of the design from the beginning rather than being added as an afterthought.

The technical architecture relies on modular, independent services with clearly defined boundaries and responsibilities. APIs implement consistent patterns and naming conventions, while comprehensive encryption and access control mechanisms protect data and resources. The architecture supports event-driven capabilities and provides various integration patterns to connect with other systems and services.

## Conclusion
The financial services industry demands infrastructure solutions that deliver exceptional performance while maintaining strict regulatory compliance and ensuring fair access for all participants. AWS Outposts racks with accelerated networking EC2 instances meet these challenges by combining capabilities of bare metal instances, specialized networking features, and precise timing mechanisms. Through accelerated networking EC2 instances, native multicast support, PTP synchronization, and equal length cabling, we provide a foundation that handles the most demanding financial applications while meeting regulatory compliance.

The static stability principle underpinning our architecture ensures operational resilience, while our proximity capabilities and direct connectivity options enable firms to maintain their competitive edge. By leveraging familiar AWS Console and API interfaces, organizations can integrate these specialized capabilities into their existing workflows while maintaining the security and consistency they expect from cloud services.

As financial markets continue to evolve and demands for lower latency and higher reliability increase, AWS Outposts racks with accelerated networking EC2 instances stand ready to support the next generation of financial innovation. Through our commitment to performance, fairness, and regulatory compliance, we’re empowering financial institutions to build and operate mission-critical systems with confidence in an increasingly dynamic market environment.