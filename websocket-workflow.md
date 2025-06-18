# Websocket Workflow

- You can underatnd websocket as a protocol which enables full-duplex (2-way connection, client & server) communication over a single TCP connection.

- You can understand the meaning of protocol is a set of rules which both client and server need to follow to communicate with each other, eg: data format/structure how to transmit between client and server.

- Advantage of using websocket:
  - Real-time communication (get updates immediately)
  - Low latency

## How does it work? (Lite version)

Here's the workflow summary:

(1). **Client Initiation**
   - Client sends an HTTP GET request

(2). **Server Response**
   - Server validates the request
   - If `accepted`, returns status code `101`

Until now, TCP/IP connection is established between client and server. Also, its bidirectional communication, which means client and server can send and receive data to each other.

(3). **Data Transmission**
   - Client listen the data which comes from server side, and if there is no data, client will keep listening
   - Server pushes latest updated data to client side if server receives any new incoming data

(4). **Connection Closure**
   - Client or server can close the connection

Code example:

```html
<!DOCTYPE html>
<html>
<head>
  <title>WebSocket Demo</title>
</head>
<body>
  <input type="text" id="messageInput" placeholder="Type a message" />
  <button onclick="sendMessage()">Send</button>
  <div id="output"></div>

  <script>
    // Connect to WebSocket server
    const socket = new WebSocket("ws://localhost:8080");

    // Event: When connection is open
    socket.addEventListener("open", (event) => {
      logToScreen("Connected to server!");
    });

    // Event: When receiving a message from server
    socket.addEventListener("message", (event) => {
      logToScreen(`Server says: ${event.data}`);
    });

    // Event: When connection closes
    socket.addEventListener("close", () => {
      logToScreen("Disconnected from server.");
    });

    // Send a message to the server
    function sendMessage() {
      const input = document.getElementById("messageInput");
      const message = input.value;
      socket.send(message);
      logToScreen(`You sent: ${message}`);
      input.value = "";  // Clear input
    }

    // Helper: Display messages on screen
    function logToScreen(text) {
      const output = document.getElementById("output");
      output.innerHTML += `<p>${text}</p>`;
    }
  </script>
</body>
</html>
```


## Short polling vs Long polling vs WebSocket

Each of them are different ways to achieve real-time communication between a client and a server.

1. Short polling: client sends request to server, and server will respond after verifying the request, and after a short period of time, the client will send another request to the server. And this process will keep repeating. (Client keep sending requests to acquire data from server side)

- (❌) Not good for real-time communication, because it keeps requesting rwsources from server, which could cause server overloaded ..

2. Long polling: the client send request to server to acquire data, so server has 2 responses:

if server has data, server will send data back to client side
else server will keep connection open and when data is available, server will send the data back to client

- (✅) Better than short polling, because it keeps the connection open until the client or server close the connection.

3. WebSocket: similar like long polling, when server side data get updated or changed, it will send latest data back to client side, the connection also kept opening until the client or server close the connection.

- (✅) Better than short polling too, because it keeps the connection open until the client or server close the connection, especially for the server pushes data to multiple clients in real-time comunication, chatting apps, etc.

