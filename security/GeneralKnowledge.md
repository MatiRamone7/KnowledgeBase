# General Security Knowledge:

## Keys / Certificates:

### Certificate:

A certificate contains a public key.
The certificate, in addition to containing the public key, contains additional information such as issuer, what the certificate is supposed to be used for, and other types of metadata.
Typically, a certificate is itself signed by a certificate authority (CA) using CA's private key. This verifies the authenticity of the certificate.

### Keys:

Every Private Key has a corresponding Public Key. The public key is mathematically derived from the private key. These two keys, together called a "key pair", can be used for two purposes: Encryption and Signing. For the purposes of certificates, signing is far more relevant.

## Keystores / Trustores:

In most cases, we use a keystore and a truststore when our application needs to communicate over SSL/TLS.

Usually, these are password-protected files that sit on the same file system as our running application. The default format used for these files was JKS until Java 8.
Since Java 9, the default keystore format is PKCS12. The biggest difference between JKS and PKCS12 is that JKS is a format specific to Java, while PKCS12 is a standardized and language-neutral way of storing encrypted private keys and certificates.

### Keystore:

A Java keystore stores private key entries, certificates with public keys, or just secret keys that we may use for various cryptographic purposes. It stores each by an alias for ease of lookup.

Generally speaking, keystores hold keys that our application owns, which we can use to prove the integrity of a message and the authenticity of the sender, say by signing payloads.

Usually, we’ll use a keystore when we’re a server and want to use HTTPS. During an SSL handshake, the server looks up the private key from the keystore, and presents its corresponding public key and certificate to the client.

Similarly, if the client also needs to authenticate itself, a situation called mutual authentication, then the client also has a keystore and also presents its public key and certificate.

(Mutual authentication is when two sides of a communications channel verify each other's identity, instead of only one side verifying the other)

- Keystore stores your credential. (server or client)	
- Keystore is needed when you are setting up the server side on SSL	
- Keystore passwords are stored in plaintext that is only readable by the specific group.
- Keystore contains private and sensitive information	

### Trustore:

A truststore is the opposite. While a keystore typically holds onto certificates that identify us, a truststore holds onto certificates that identify others.

In Java, we use it to trust the third party we’re about to communicate with.

- Truststore stores others credentials (CA)
- Truststore setup is required for the successful connection at the client side
- Truststore passwords are stored in plaintext that can be read by everyone.
- Truststore doesn’t contain private and sensitive information

Example:
If a client talks to a Java-based server over HTTPS, the server will look up the associated key from its keystore and present the public key and certificate to the client.
We, the client, then look up the associated certificate in our truststore. If the certificate or Certificate Authorities presented by the external server isn’t in our truststore, we’ll get an SSLHandshakeException, and the connection won’t be set up successfully.


## X509 Certificate:

Certificates that follow the X.509 standard contain a data section and a signature section. The data section includes such information as:

- The Distinguished Name of the entity that owns the public key
- The Distinguished Name of the entity that issued the certificate
- The period of time during which the certificate is valid
- The public key itself

Protocols: SSL/TLS, SSH, PGP
Encryption algorithms: RSA, ECC


## File extensions:

- .pem: A .pem is a de-facto file format called Privacy-Enhanced Mail. A PEM file can contain a lot of different things, such as certificates, private keys, public keys and lots of other things. A file being in PEM format says nothing about the content, just like something being Base64-encoded says nothing about the content.
- .crt, .cer: This is another pseudo-format that is commonly used to store certificates. These can either be in the PEM or in the DER format.
- .p12, .pfx: These are interchangable file extensions for the PKCS#12 format. Technically, PKCS#12 is the successor to Microsoft's PFX format, but they have become interchangable. PKCS#12 files are archives for cryptographic material. Again, what kind of material this contains is completely up to the user.

Yes, .crt, .pem, .pfx and .p12 can all be used to store certificates, public keys and private keys. From a purely technical standpoint, you can not tell what the semantic content of any of these files is just by their file extension. 

However, there are some common conventions that are being followed. .p12 and .pfx files are usually used to store a certificate together with the private key that corresponds to this certificate.

Likewise, .crt files usually contain single certificates without any related private key material.

.pem files are wildcards. They can contain anything, and it's not uncommon to see them used for all different kinds of purposes. Luckily, they are all plain text, and are prefixed in a human-readable way, such as


https://www.baeldung.com/java-keystore-truststore-difference
https://www.baeldung.com/cs/public-private-keys-vs-certificates
https://security.stackexchange.com/questions/226747/what-is-the-difference-between-a-certificate-and-a-private-key
https://www.techtarget.com/searchsecurity/definition/mutual-authentication
