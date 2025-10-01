# API Gateway

## What is an API Gateway?

- API Gateway is a single entry point and routes the API requests to backend services
- Can be understood as a `middleware` that sits between clients and backend services

Use it when you have multiple services and want to centralise access, authentication, logging, and request handling.

## What are the key features of an API Gateway?

- Routing (Eg: From `v1/feeds` -> looking for -> `feed-service.prod.svc.cluster.local:8080`)

```
Client Request: GET https://api.your-app.com/v1/feed?page=1
    ↓
[API Gateway]
    ↓
Route: /v1/feed* → feed-service.prod.svc.cluster.local:8080
    ↓
[Feed Microservice] handles the request
```

- Request/Response transformation (API response)
- Rate limiting (Please refer to [Rate Limiting Note](./rate-limiting.md) for more details)
- Authentication
- Load Balancing (Distributes traffic across service instances)

## Tools:

- AWS API Gateway
- Azure API Management
- Google Cloud Endpoints
- Kong
