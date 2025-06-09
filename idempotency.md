# Idempotency

## What is idempotency?

- Idempotency refers to certain operations can be safely repeated without unintended side effects. (eg: Usage for API design)

- Ensure actions not repeated unintentionally (eg: handle retries)

## Examples:

(1). For HTTP methods:

- Idempotent: GET, PUT, DELETE, HEAD, OPTIONS

Calling DELETE /users/123 multiple times will delete the user once, then return the same success (or 404) response

- Non-idempotent: POST, PATCH

Each POST /users creates a new user with a new ID


(2). For Database:

- Idempotent: INSERT, UPDATE, DELETE

```sql
UPDATE users SET status = 'active' WHERE id = 1 (idempotent)
```

- Non-idempotent: CREATE TABLE, DROP TABLE

```sql
INSERT INTO users (name) VALUES ('John') (non-idempotent)
```

(3). For APIs:

- Add idempotency keys: 

```javascript
// Client-side implementation
const idempotencyKey = crypto.randomUUID();

fetch('/api/payments', {
  method: 'POST',
  headers: {
    'Idempotency-Key': idempotencyKey, // add unique key for each request
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ amount: 100 })
});
```

## Usage:

- Payment processing (preventing duplicate charges)
- Stock trades (ensuring single execution)
- Blockchain transactions (nonce mechanisms)


## For a specific example: SMS notifications

- Idempotent: Sending the same SMS multiple times will not send the same SMS multiple times

How?

Gateway level deduplication

```javascript
// Using Twilio-like API with MessageSid
POST /api/sms
{
  "to": "+15551234",
  "body": "Your code is 1234",
  "message_id": "client-generated-uuid"
}

// Server-side
if (SMSSentLog.exists(message_id)) {
  return cached_delivery_status;
}
```

Time-window blocking

```javascript
// Prevent same content to same number within X minutes
const recent = await SMSLog.findOne({
  to: request.to,
  body: request.body,
  sent_at: { $gt: new Date(Date.now() - 30*60*1000) }
});
```
