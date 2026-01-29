## Bandit level 15

### goal
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

### theory
OpenSSL is a library for secure communication over networks. It implements the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) cryptographic protocols that are, for example, used in HTTPS to secure the web traffic.

openssl s_client is the implementation of a simple client that connects to a server using SSL/TLS.

## sol
Since the task states that the password can be retrieved using SSL encryption, I connect to the localhost server with the OpenSSL client and send the password from this level. The server then sends back the password for the next level.

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
...
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
```