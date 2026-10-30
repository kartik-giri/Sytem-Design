# What is HTTP and HTTPS?
- Http stands for hyper text transfer protocol.
- It alows the client and server to exchange data to each on single connection.
- But the data transfer through http is not secure it can be looked by hackers and hacker can read user credentials.

- SO the solution is Https.
- HTTPS stands for HTTP + Transport layer security.
- Https encrypts the data and provide data integerity means it detects if data was modified while transit? 
- And HTTPS also hrlps the browser in verifing the erver asocciated with the domain
- HTTPS uses TLS handshake to create the secure connection between client and server.
- The clinet first sneds the hello to the server.
- The server accepts the hellp from client and sends its certificate to browser.
- The browser validates the certificate and secure connection is established.


### What is HTTP and HTTPS?

- HTTP stands for **Hypertext Transfer Protocol**. It is an application-layer protocol that allows clients and servers to communicate through requests and responses.
- HTTP does not encrypt the data being transferred. Therefore, an attacker who can intercept the traffic may be able to read sensitive information, such as credentials.

**HTTPS (HTTP Secure)** is HTTP secured using TLS (Transport Layer Security).

HTTPS provides three security properties:
1. **Confidentiality:** Encrypts data so unauthorized parties cannot read it.
2. **Integrity:** Detects whether data has been modified during transmission.
3. **Authentication:** Helps the browser verify the server's identity using its TLS certificate.

### How does the TLS handshake work?

1. The client sends a `ClientHello` message containing supported TLS versions, cipher suites and key-share information.
2. The server responds with `ServerHello` and sends its TLS certificate.
3. The browser validates the certificate, including its domain name, validity and certificate trust chain.
4. Both client and server establish shared encryption keys.
5. Encrypted HTTP communication begins.

Therefore, HTTPS protects communication between the client and server against eavesdropping and tampering.