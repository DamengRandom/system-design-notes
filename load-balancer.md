# Load Balancer

## What is load balancer?

- Load balancer: distributes the network traffic across multiple servers to improve performance (`faster response time`) and reliability (no single point of failure)

- Common ways to share the traffic: round-robin, least connections and IP hash, consistent hashing and etc
  - `Round-robin` [static alogirthm]: its like a poker game, which forward requests round by round (Common)

  - `IP hash` [static alogirthm]: send the request to the server with the same IP address, same user request will always to be forwarded to the same server

  - `Least connections` [dynamic alogirthm]: send the request to the server with the least number of connections (most idle server first considered), the least, the higher priority to get the user requests

  - `Least Response Time` [dynamic alogirthm]: the most fast response server will get the chance to handle the requests first ~

- Load balancers will ping servers regularly to ensure they are up (`health check` ❤️) before sending traffic to them

- For OSI 7 layers, application, network, transport and data link layers can do load balancers, for web development, we normally focus on application layer

- Metaphor: Its like a `traffic controller`, it will distribute the cars to different roads to drive, and try the best to avoid the traffic jam occurred

- Question: what is relationship between the reverse proxy server and load balancer?
  Answer: 
    - `Reverse proxy server`: it will receive the request from client, and forward the request to backend server, and return the response to client (One of common: `Nginx`)
      - Another explanation: Its sit iun front of backend servers and represent them to the clients
    - `Load balancer`: it will distribute the traffic to multiple backend servers, and return the response to client


## Technologies:

- `Nginx`: open source, high performance, scalable, used as a web server, reverse proxy, load balancer
- `AWS ELB`: Elastic Load Balancer, managed by AWS

## Redundancy:

- To add redundancy, we can use multiple load balancers, which will distribute the traffic to multiple servers (when one load balancer is down, the rest still functional, think about airplane turbo engines, when one is down, another one still functional, airplane still can fly ~)

