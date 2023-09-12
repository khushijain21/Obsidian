
When a website visitor tries to open a website, their web browser engages in a process with the website’s server that’s known as a TLS handshake. As part of this process, the browser (client) generates a random pre-master secret, encrypts it using the server’s public key, and sends it to the server. The server decrypts the pre-master secret using the corresponding private key and uses it to compute a symmetric session key.

All the data transferred between a user and a website for the rest of the session is encrypted using the session key — meaning that it’s transmitted via symmetric encryption. No intruder can access the session key without a private key. It’s this initial use of public key cryptography that makes it possible to exchange session keys to engage in symmetric encryption for the rest of the session. This process protects data transmissions between a website and its visitors.




