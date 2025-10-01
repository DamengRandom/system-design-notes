# Load Balancer

## What is load balancer?

- Load balancer: distributes the netwrok traffic across multiple servers to improve performance (`faster response time`) and reliability (no single point of failure)

- Common ways to share the traffic: round-robin, least connections and IP hash, consistent hashing and etc
  - Round-robin: each request is sent to a different server, follow the sequence of servers, when reaches to the last server, it will start from the first server again

  - Least connections: send the request to the server with the least number of connections, the least, the higher priority

  - IP hash: send the request to the server with the same IP address

  <!-- - Consistent hashing:
    - Hash the request to a specific server
    - When a server is added or removed, the hash will be re-calculated, which will affect the distribution of the traffic  -->

- Load balancers will ping servers regularly to ensure they are up before sending traffic to them


## Technologies:

- Nginx: open source, high performance, scalable, used as a web server, reverse proxy, load balancer
- AWS ELB: Elastic Load Balancer, managed by AWS

## Redundancy:

- to add redundancy, we can use multiple load balancers, which will distribute the traffic to multiple servers (when one load balancer is down, the rest still functional, think about airplane turbo engines, when one is down, another one still functional, airplane still can fly ~)

