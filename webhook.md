# Webhook

## What is webhook?

- Webhook is a way to notify a server when an event occurs.
- [Event occurs] -> [Provider sends HTTP POST request] -> [Your Server process the request]
- Normally client has a url and server will call that url to notify the client when an event occurs.

## Why use webhook?

- Webhook enables real-time communication, because webhook puahes data instantly when and event occurs.

Eg: Instead of keep polling/requesting data from server, webhook notify you immediately when data event triggered (data is available)

Real-time notifications, payments, CI/CD, etc.

- Advantage of using webhook: reduce the number of requests to the server, reduce the latency, reduce the load on the server, etc.
