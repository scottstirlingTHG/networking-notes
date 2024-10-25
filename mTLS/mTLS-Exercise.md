# mTLS Notes

## Quick review of TLS

As a quick reminder TLS (Transport Layer Security) is a cryptographic protocol that helps us send encrypted messages thrpugh the internet. The most widely known implementation of the TLS is the HTTPS which you can see being employed across the web. 

### The TLS handshake

The TLS connection starts it initiated the TLS handhsake where several key decisions (excuse the pun) are made. First the client sends a "ClientHello" message to request a secure website. This message comes with information about which versions of TLS it can use and the which cipher suites[^-1] that can be used.

[^-1]: A cipher suite is a collection of cryptographic algorithms that will be used create the necessary keys and encrypt infromation.

The Server responds with it's "ServerHello" message which includes the highest version of TLS and cipher suites that both support. It then also passes along the servers digital certificate which has been verified by a Certificate authority.

The client then verifies the servers certificate and then uses the servers public key to encrypt a "premaster secret" and send to the server. Once the server decrypts the premaster secret (using the private key) both parties then make their sessions keys and then use symmetric encryption for subsequent communication.

## Moving onto mTLS

You may have noticed during TLS that the server never checked that the client was authenticated and only the authenticity of the server was checked. This is the point of distinction between mTLS (mutual TLS) and TLS, both parties are authenticated. It does this by having both parties presenting their certificates to each other in order for authentification to take place.

You would use mTLS is a setting where there is a zero trust framework where no devices on a network are trusted. An example of an application which uses this is Cloudflare Zero Trust (I am checking if Okta on our laptops uses mTLS - I suspect it does).

### How does it work?

Like TLS, mTLS makes use of public key cryptography in order to securely transfer information to establish symmetric encryption. 
Similar to TLS the the public keys are part of the certifcate. In the following steps we will outline mTLS while abstracting away some of the public key details.

1. First the client sends the ClientHello to the server. 

2. The Server then responds with the ServerHello. 

3. The server then follows this up with sending their certificate. 

4. The client then checks this against the chain in order to establish trust. 

5. Once verified the server request the clients certificate and then sends cryptographic information in order for the server to verify the cleints certifcate. 

6. They then generate their agreed upon symmetric encryption and then proceed using that for all communication in the session.


### Why not always use mTLS?

mTLS is more secure than regular TLS so why do we not always use it when we accessing a webpage, there are two main reasons for this:

- It is more costly than regular TLS.

- For websites we only really care about the servers identity as the client only needs to know the legitimacy of the server.


### When to use mTLS?

- B2B finance - We would use mTLS in order to securely transactions between two businesses

- Securing APIs - making sure the API can veryify who is trying to get access and also the client can verify where they are getting the information from.

### What does mTLS with?

- On-Path attacks (Man in the Middle) - The encryption stops anyone being able to read the information.

- Spoofing attacks - For isntance a server will not be able to fake it is another server since each side is authenitcated (I think TLS stops this too).

- Credential stuffing -  without a legitmate certificate the leaked credentials are less useful in gaining access.

- Phishing attacks - Like the above stolen credentials are less useful since the certifcate is still needed for access

- Malicious API request - Since the API needs users to be authenticated via certificate request can only be made from authenticated users.


### Bibliography

- https://www.cloudflare.com/en-gb/learning/access-management/what-is-mutual-tls/

- https://builtin.com/software-engineering-perspectives/mutual-tls-tutorial

- https://www.securew2.com/blog/mutual-tls-mtls-authentication

- https://www.cloudflare.com/en-gb/learning/ssl/transport-layer-security-tls/






























