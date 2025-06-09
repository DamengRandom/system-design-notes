# System Design

## Grabbing business requirements

- Functional requirements
- Scope the problem
- Non-functional requirements

## Key topics

- Scalability: how to handle the increasing load
- Reliability: how to handle the failure
- Maintainability: how to maintain the system (especially when new developers join the team)
- Efficiency: how to take good advantage of the resources

## Data interactions

- Moving data: take data from one place to another without any issue
  - API requests, eg: user fetching, data from DB A to DB B and etc

- Storing data: store data in a way that is easy to retrieve
  - Database choice:
    - SQL database: relational database, eg: MySQL, PostgreSQL etc.
    - NoSQL database: non-relational database, eg: MongoDB, Cassandra etc.
  - Key topics:
    - Access patterns
    - Indexing stratgies
    - Backup solutions

- Transforming data: change the data in a way that is easy to retrieve
  - transfer raw data to a meaningful information


## CAP Theorem

- Consistency: all nodes see the same data at the same time (one node is updated, then all nodes will see the updated data too)

- Availability: the system is always available (even if some nodes are down, eg: 24/7 support) [Downtime measurement in milliseconds] [Consideration factors: downtime (fault tolerance), backup (reliability), redundancy, etc]

- Partition tolerance: the system can continue to operate even if some nodes are down during the network failure (eg: think like Cisco routers, switches setups, we need to consider the redundency of the network, ensure one or few nodes are down, communication is still available in the system)


## Speed

- Throughput: how many requests can the system handle per second (eg: Server RPS, Database throughput, eg: QPS, another data throughput, B/s)

- Latency: how long it takes to process a single request (eg: Server Latency) [btaching process can increase throughput, but it will increase latency, thats why we need trade-off solution for the specific use case]


## IP address

How computer communicate with each other?

- IP address: 
  - IPv4: 32 bits, eg: 192.168.1.1
  - IPv6: 128 bits, eg: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

  Inside IP header, it stores the source and destination IP address.

- Port: 
  - 0-65535, eg: 80, 443

## TCP (Transmission Control Protocol) - Transport layer

- TCP header indicates the source and destination port number
- 3-way handshake: SYN, SYN-ACK, ACK (used for eastablish the connection between 2 devices)

## UDP (User Datagram Protocol) - Transport layer

- UDP is used for real-time or time sensitiveapplications, eg: video streaming, voice calls, gaming etc
- UDP is a connectionless protocol, it does not guarantee the delivery of the packet, it is faster than TCP

## DNS (Domain Name System) - Application layer

- DNS is used to translate/map the domain name to the IP address (A Record)
- For AAAA record, it is used to translate/map the domain name to the IPv6 address


## Protocols:

- HTTP: Hypertext Transfer Protocol: used for web communication
- HTTPS: Hypertext Transfer Protocol Secure: used for web communication with encryption
- FTP: File Transfer Protocol: used for file transfer
- SMTP: Simple Mail Transfer Protocol: used for email communication
- POP3: Post Office Protocol 3: used for email retrieval
- IMAP: Internet Message Access Protocol: used for email retrieval
- DHCP: Dynamic Host Configuration Protocol: used for network configuration
- MQTT: Message Queuing Telemetry Transport: used for IoT communication (lightweight, pub/sub, publish-subscribe)
- WebRTC: Web Real-Time Communication: used for real-time data communication (enable browser-to-browser communication, eg: voice call, video call, file sharing, etc)

and so on ...

To be continued ...
