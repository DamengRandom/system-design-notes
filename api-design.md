# API Design

In this note, we just focus on RESTful API design.

## RESTful API Considerations

- Consistency & Predicatability
  - Follow the RESTFul conventions for handling CRUD operations
  - Use HTTP methods to represent the action (GET, POST, PUT, DELETE, PATCH)
  - Maintaining consistent naming, eg: `/users` (✅) instead of `/getUsers` (❌)
  - Return uniform response structures, eg: data, error, status fields as part of the API response

- Simplicity
  - Use nouns instead of verbs
  - Avoid deep nesting of resources, eg: `/users/1/orders/{orderId}/items` (❌) instead of `/users/1/orders` (✅)

- Versioning
  - URL versioning: `api/v1/users`
  - Header versioning: eg: Accept: `application/vnd.company.v1+json`
  - Query parameter versioning: eg: `api?version=1.0`

- Documentation
  - Use Swagger or OpenAPI to document the API (Provide clear and concise documentation for the API)

- Proper Status Codes
  - Return proper status codes for the API design, eg following: 200, 201, 204, 400, 401, 403, 404, 500
  - User will be able to know exact status of the request

- Error Handling
  - Return proper error messages for the API design, eg: `{ "error": "Invalid request" }`
  - User will be able to know exact error message

- Pagination
  - For large datasets, return a subset of the data, eg: `{ "data": [...], "total": 100, "page": 1, "limit": 10 }`
  - Examples:
    - Pagination: `?page=1&limit=10`
    - Filtering: `?status=active`
    - Sorting: `?sort=-created_at`
    - Search: `?search=John`

- Caching
  - For reducing the latency
  - Implement caching to improve performance, eg: `Cache-Control: max-age=3600`
  - CDN (Content Delivery Network) to improve performance, eg: `CDN-Cache-Control: max-age=3600`

- Idempotency
  - Add idempotency key to the request, eg: `X-Idempotency-Key: 1234567890` as part of request header (Never change the result of the via multiple duplicated API requests)

- Security
  - Use HTTPS to secure the API
  - CORs support (Cross-Origin Resource Sharing, controls which domains can access the API)
  - Rate limiting to prevent abuse (prevent DDoS attack)
  - Input validation to prevent malicious requests, (eg: ajv, zod, etc)
  - Authentication to prevent unauthorized access, (eg: JWT token, OAuth2, etc)
  - Authorization to prevent unauthorized access, (eg: RBAC, ABAC, etc)

- Performance
  - Use caching to improve performance, eg: `Cache-Control: max-age=3600`
  - Use compression to improve performance, eg: `Content-Encoding: gzip`
  - Use CDN to improve performance, eg: `CDN-Cache-Control: max-age=3600`
  - Use load balancing to improve performance, eg: `X-Forwarded-For: 192.168.1.1`

- Backward compatibility
  - Add a new versioning to the API, eg: `api/v2/users` (Don't break existing API, eg: `api/v1/users`)
  - Add deprecation notice to the API, eg: `This endpoint is deprecated, please use the new endpoint`


## A quick compare between different API paradigms:

REST:
  - Pros:
    - Stateless, easy to implement
    - Standard HTTP methods (GET, POST, PUT, DELETE, PATCH)
    - JSON for data exchange
    - Well-documented and supported
  - Cons:
    - Over-fetching: returning more data than needed

GraphQL:
  - Pros:
    - Client-driven data fetching (using query language to fetch data)
    - Avoid over-fetching and under-fetching (by defining the schema)
    - Better performance
  - Cons:
    - Complexity: query could impact the server performance

gRPC:
  - Pros:
    - Multiplexing / Server push
    - Uses protocl buffers
    - Efficiency
  - Cons:
    - less human readable
    - only support HTTP/2 protocol
