# REST APIs

REST APIs are called "REST APIs" because they are designed following the principles of REST (Representational State Transfer), which is an architectural style for designing networked applications. REST was introduced by Roy Fielding in his 2000 doctoral dissertation as a set of guidelines and constraints for building scalable and performant web services.

## Breakdown of the Term
### Representational:

- Resources (e.g., data or objects) in a RESTful system are represented using a standardized format like JSON, XML, or HTML.
- For example, a resource like a "user" might be represented in JSON format as:

```json
{
  "id": 1,
  "name": "Alice",
  "email": "alice@example.com"
}
```

###  State Transfer:

- The client (e.g., a web browser or mobile app) and server communicate through requests and responses.
- Each request from the client to the server contains all the information needed to understand and process it, making the system stateless.
- Any "state" of the client, such as authentication or session data, is either stored on the client or passed explicitly in the request (e.g., through tokens or cookies).

## Why "REST"?
The name reflects the following principles of REST:

### Resource-Oriented:

REST treats everything (e.g., a user, product, order) as a resource.
Resources are identified by URIs (Uniform Resource Identifiers), such as:
```bash
/users/1
/products/123
```

### Stateless Communication:

Each request from the client is self-contained and does not rely on the server remembering previous interactions.
This simplifies the server design and improves scalability.

### Uniform Interface:

- REST APIs use standard HTTP methods to interact with resources:
- GET: Retrieve a resource.
- POST: Create a new resource.
- PUT: Update an existing resource.
- DELETE: Delete a resource.

e.g.:
- GET /users/1 → Fetch user with ID 1.
- POST /users → Create a new user.

### Statelessness:

No client state is stored on the server.
Each request includes all the necessary information, such as authentication tokens.

### Layered System:

A RESTful API can be designed to work through multiple layers (e.g., proxies, gateways) without affecting the communication between the client and the server.

### Cacheability:

Responses from the server can be marked as cacheable, allowing clients to reuse data without making repetitive calls.

### Code on Demand (Optional):

REST allows servers to send executable code (like JavaScript) to the client to extend its functionality dynamically.