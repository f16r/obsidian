# Reverse Proxy
- Sits in front of backend servers forwarding requests from a client
- Hides servers from client
- decides which backend server should handle the request based on rules
- Useful for load balancing, caching, security (filtering out requests), centralized authentication, Compression (compression responses, requests)
- Nginx, CDNs

Client (Browser)
      |
      v
+-----------------+
|  Reverse Proxy  |
+-----------------+
   |          |
   v          v
Backend 1   Backend 2
(Server A)  (Server B)
# Forward Proxy
- Hides client from server by acting as middle man
- Client sends request to proxy instead of directly requesting the service
- Proxy makes the request on behalf of the client and returns the response once retrieved
- Useful for Anonymity, access control (e.g. block/allow traffic), caching, content filtering, bypassing restrictions (geoblocking)

Client (Browser)
      |
      v
+----------------+
| Forward Proxy  |
+----------------+
      |
      v
 Destination Server (e.g., example.com)