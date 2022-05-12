### Public-Key (Asymmetric) Cryptography

A public key or asymmetric cryptographic system uses pairs of keys. One key is a *private key* (known only to its owner) and the other is a *public key* (which can be publicly distributed). The keys are related but play different roles, which is why these are often called *asymmetric cryptography*. It is vital in these systems to keep the private key private.

These algorithms can be used in one or more ways (depending on the algorithm), including:

* **Encryption**
Anyone could encrypt a message using a public key, but only someone with the corresponding private key could decrypt it. Public key encryption algorithms are generally relatively slow, so in many situations, a *key* for a shared-key algorithm is encrypted, and the rest of the message is encrypted with a shared key.

* **Digital signatures (authentication)**
A sender can use a public key algorithm and their private key to provide additional data called a *digital signature*; anyone with the public key can verify that the sender holds the corresponding private key.

* **Key exchange**
There are public key algorithms that enable two parties to end up with a shared key without outside passive observers being able to determine the key.

A widely-used public key algorithm is the RSA algorithm, which *can* be used for all these purposes. However, *do not implement RSA yourself*. RSA is fundamentally based on exponentiation of large numbers, which lures some developers into implementing it themselves or thinking it is simple. In practice it is extremely easy to implement RSA *insecurely*. For example, it is very difficult to check for weak parameters that *look* acceptable but make it trivial to defeat. To be secure, RSA *must* be implemented with something called “padding”. There is a standard RSA padding scheme with a rigorous proof called OAEP, but it is difficult to implement correctly (incorrect implementations may be vulnerable to *Manger’s attack*). In practice, RSA can be tricky to apply correctly, and unless you understand cryptography, you won’t be able to tell when it is not working ([*Seriously, stop using RSA*](https://blog.trailofbits.com/2019/07/08/fuck-rsa/), 2019).

RSA key lengths need to be longer than you might expect. An RSA key length of 1024 bits is approximately equivalent to a symmetric key length of 80 bits, which is so small that it is generally considered insecure. An RSA key length of 2048 bits is equivalent to a symmetric key length of 112 bits; a 2048 bit is considered barely acceptable by some (e.g., NIST says that this may be used through 2030, after which it may not be used by the US government). If you are using RSA, you should probably use at least 3,072 bit key in current deployments (this is equivalent to a 128 bit symmetric key). You would need an RSA key of 15,360 bits to get the equivalent of a 256-bit symmetric key. See [NIST’s *Recommendation for Key Management: Part 1 - General*](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf) for more about key equivalent lengths. Unfortunately, RSA is relatively slow, especially as you increase to key lengths necessary for minimum security. For all these reasons, some organizations, such as Trail of Bits, recommend avoiding using RSA in most cases ([*Seriously, stop using RSA*](https://blog.trailofbits.com/2019/07/08/fuck-rsa/), 2019).

A whole family of algorithms are called *elliptic curve cryptography*; these are algorithms that are based on complex math involving elliptic curves. These algorithms require far shorter key lengths for equivalent cryptographic strength, and that is a significant advantage. Historically, elliptic curve cryptography involved a minefield of patents, but over the years many of those patents have expired and so elliptic curve cryptography has become more common. A widely-used and respected algorithm for key exchange and digital signatures is Curve25519; a related protocol called ECIES combines Curve25519 key exchange with a symmetric key algorithm (for more details, see [*Seriously, stop using RSA*](https://blog.trailofbits.com/2019/07/08/fuck-rsa/), 2019).

The Digital Signature Standard (DSS) is a standard for creating cryptographic digital signatures. It supports several underlying algorithms: Digital Signature Algorithm (DSA), the RSA digital signature algorithm, and the elliptic curve digital signature algorithm (ECDSA).

There are also a variety of key exchange algorithms. The oldest is the Diffie-Hellman key exchange algorithm. There is a newer key exchange algorithm based on elliptic curves, called Elliptic Curve Diffie-Hellman (ECDH).

As hinted at earlier, it is critical that you use existing well-respected implementations (don’t implement it yourself), and check any parameters you choose carefully. Perhaps the most important is the key length for that algorithm (as noted earlier, elliptic curve algorithms have equivalent strength with shorter keys). A useful source for recommended key lengths is [NIST’s *Recommendation for Key Management: Part 1 - General*](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf).