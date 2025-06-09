# Rate Limiting

## What is rate limiting?

- Rate limiting is a technique used to control the rate of requests to a service.
- It is used to prevent abuse of the system, also maintain reliability and fairness.


## Why rate limiting is important?

- Prevent abuse of the system
- Maintain reliability and fairness
- Prevent unexpected bills by abuse the service
- Reduce server load in order to prevent server crash during high spikes of requests


## Rate limiting vs Quotas

- Rate limiting: controls how often you can make an API request (eg: 10 requests per second)
- Quotas: controls how much you can consume over a long period (eg: 1000 requests per day)


## Types of rate limiting

- Token bucket: each request needs a token to proceed, tokens are refilled at a fixed rate
- Fixed window: Count requests oer user Ip addeess in fixed time blocks
- Sliding window: momery intensive, logs timestamp of each request and checks how many occurred in the last X seconds
- Leaky bucket: similar like a queue, requests are processed at a constant rate. Excess requests are dropped.
