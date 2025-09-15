# API Fesign Version 2 (Keep agiling the understanding ...)

- API (Application Programming Interface) design could be divided into few steps during system design interview
  - REST vs GRAPHQL vs RPC
  - RESTful API design: default/normal and common choice, eg: `GET /api/users`
  - GraphQL API design: fetch specific data structure based data to frontend, eg: `{ users { id, name, email } }`
  - RPC API design: fast, but less flexible, eg: `call getUser(id: 1) { id, name, email }`

## RESTful API:

Brief points (Partial):

- No verbs!! Methods itself represent for the verb, such as `GET/POST/PUT/PATCH/DELETE`, eg: `GET /api/v1/users` (✅), no `POST /api/v1/users/create` (❌)

- Path Parameter, Query Parameter, Request Body, Response Body, Status Code, Headers:
  - Path Parameter: eg: `GET /api/v1/users/{id}` -> specify which resource you're working with
  - Query Parameter: eg: `GET /api/v1/users?page={number}&limit={number}` -> use as optionl filters with `?` and `&`
  - Headers: eg: `Content-Type: application/json`
  - Request Body: eg: `POST /api/v1/users` with `{ name, email }` (usually JSON payload)
  - Response: 
    - Response Body: eg: `{ id, name, email }` (usually JSON payload)
    - HTTP Status Code: eg: `2xx`, `3xx`, `4xx`, `5xx`, etc.

## GraphQL:

- basic structure example:

```graphql
# POST /graphql
# Content-Type: application/json
{
  query {
    users {
      id
      name
      email
      age
      address {
        city
        country
      }
      phoneNumbers {
        number
        type
      }
    }
  }
}
```

key points: 

- Customised data sturcture !!
- All requests in one query (Better keep query not too big, perofrmance considerations) ~~

## RPC:

- Mainly service to service communication !!
- An external API, which is used for intra-microservice communication (Efficient solution !!)

Pitfall point: not good for client and server communication because of client can be variety of devices, such as mobile, desktop browsers, not recommanded for client - server communication!!

- Examples:
<!-- instead of GET /api/v1/users/123 -->
getUser(id: 123)
<!-- instead of POST /api/v1/users/123/bookings -->
createBooking(eventId: 123, userId: 123)

- basic code example:

```rpc
service UserService {
  rpc GetUser (GetUserRequest) returns (User) { ... }
  rpc CreateBooking (CreateBookingRequest) returns (Booking) { ... }
}

message GetUserRequest {
  int32 id = 1;
}

// strong typed definitions
message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
}
```

You could imagine this is how python server can talk to another go server, mutiple languages can communicate, like a MCP concept,

RPC will take the role which handles the network communication under the hood for both servers can talk with each other with RPC interface !!!


## Some other small concepts:

- Why pagination: for handling tons of data with a limited range of data fetching ~

- Basic security consierations:
  - `JWT token` -> plus refresh token which enable long term authentication (self-prefer)
  - `Session token` -> from server side generate a random token within API request for authentication purpose as well
  - `HTTPS` -> encrypt the data transmission (secure client-server communicatoin consideration)
  - `Input validation` -> prevent injection attack
  - `Rate limiting` -> prevent brute force attack
  - `Authorization` -> ensure only authorised user can access the resource
