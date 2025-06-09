# Mock Twitter 

## Functional requirements

- User can create an account
- User can login
- User can create a post
- User can view a post
- User can follow a user
- User can unfollow a user

## Non-functional requirements

- The system should be easier to scale 1M of users
- Also able to handle high volume of tweets, likes, and so on
- Low latency for the system
- High availability for the system
- Secuirty considerations


## Workflow

Client -> Load balancer (Round-bin) -> API gateway (forward request to the servers) -> 

1. Tweet/Reply CRUD service
  - Save tweet textable contents into a non-relational database (NonSQL: MongoDB), faster I/O operations
  - Save tweet media contents into a object storage into AWS S3 (faster read purpose)
  - Add a rate limiter for writing operations, so which aims to prevent DDoS attack, prevent unexpected bills by abuse the service and reduce server load in order to prevent server crash during high spikes of requests
  - Provide a cache for reading the popular tweets, also fast reading purpose
  - Add a CDN (to users geographic area) for media contents, which is faster to read the media contents (reduce latency)

  - Similar thing, we add rate limiter for write replies service, which is to prevent abuse of the service, and also reduce server load in order to prevent server crash during high spikes of requests
  - Save replies to a different database, so we read the data seprately from different places by Frontend
  - Eventually, we are going to bind a tweet with media contents and replies all together before sending over to the frontend side. How? By doing `indexed by Tweet Id for the fast look up`

  - Last but no least, we need to add `timeline fanout write` service for handling the new created tweets,
    - so all the new created tweets will be sent to the message queue, 
    - then, the timeline `fanout` service will read the messages from the messages queue, the job is dne by the `workers` (workers can be scaled based on how havey the traffic is)
    - and then, the followers will be notified by the `timeline cache`, so the followers can read the tweets from the `timeline cache` (everytime, the new tweets will be waiting for the followers to read, which is extemely fast, because data is waiting inside cache)
    - So now, the `timeline service` is going to read the tweets from the `timeline cache` and send over to the frontend side
    - Also, the `timeline service` is also able to read the tweets from the tweets contents DB, (we do as a `separate` appraoch) for the popluar tweeters, eg: Elon, John, etc, so the `timeline cache` will not be abused or overloaded by the popular tweeters (since they have more followers)


2. Search/Follow/Unfollow/Timeline service
  - Establish a ElasticSearch database for the fast text search (search for the tweets specifically) [low latency], so the search service will connect with ElasticSearch database for fetching the searched result of the tweet(s)
  - Meanwhile, we need to use a technique called `CDC` (Change Data Capture) to sync thge database between (NonSQL: MongoDB) and ElasticSearch database, so the data is synced (real-time)

  ```yaml
    PostgreSQL
    |
    | (CDC - WAL)
    v
  Debezium Connector (Kafka Connect)
    |
    v
  Kafka Topic (e.g., dbserver1.inventory.customers)
    |
    v
  Kafka Connect Elasticsearch Sink Connector
    |
    v
  Elasticsearch Index (e.g., customers)
  ```
  

3. Profile service
  - Handle user data to create a new profile `gragh` DB, for later on `recommandations` feature development 
  - Need to add a Auth service to handle the user authentication, authorization and account (permission maybe) management (security considerations)
  - Add input validations for input (correct data pass through)

-> Establish a CDN to client website, so user can read the website faster (reduce latency)

-> Add some observability for the system, like metrics, logs, etc, so we can monitor the system and make sure the system is running smoothly, eg: Health checks, Logging, alerts (bug/error detection) tools: 
  - Prometheus: collect metrics from the system
  - Grafana: visualize the metrics
  - ELK: collect logs from the system
  - Kibana: visualize the logs

-> Testings considerations:
  - Unit tests: test the individual components of the system
  - Integration tests: test the interaction between the components of the system
  - End-to-end tests: test the entire system
  - Load tests: test the system under load
  - Stress tests: test the system under stress
  - Security tests: test the system under security


## Diagram ~

![Twitter Mock](/Images/twitter-mock.png)

<!-- Press Ctrl / CMD + Shift + V to preview the MD document inside VSCode, Cursor -->