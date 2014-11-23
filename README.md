Check That Cert!
=============

Unless you verify who you are talking to, having an encrypted channel won't provide you confidentiality or integrity. Not checking the SSL certificate of a remote server you are communicating with allows anyone with control of the network to stand up their own server and certificate, impersonating your server.

# Generating a self signed certificate

````
openssl genrsa -out server.pem 4096
openssl req -new -x509 -key server.pem -out cert.pem -days 30
````

Sample output:

````
[user@localhost testcase]$ openssl genrsa -out server.pem 4096
Generating RSA private key, 4096 bit long modulus
....................................................................................++
...........................++
e is 65537 (0x10001)
[user@localhost testcase]$ openssl req -new -x509 -key server.pem -out cert.pem -days 30
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:Washington
Locality Name (eg, city) [Default City]:Seattle
Organization Name (eg, company) [Default Company Ltd]:Check That Cert
Organizational Unit Name (eg, section) []:Testcases
Common Name (eg, your name or your server's hostname) []:localhost
Email Address []:someone@example.com
[user@localhost testcase]$ 
````

## Hosting a simple server to test encrypted communication

````
openssl s_server -tls1 -tls1_1 -tls1_2 -key server.pem -cert cert.pem -www
````


# What needs verification?

## Hostname

The hostname (or CN) is a commonly accepted way of identifying the name of the system you are communicating with. In the event that an attacker redirects your traffic to another system trusted by client, validation of the hostname will prevent the transport from operating to the incorrect service.

## Issuer

## Valid from-to timestamps

## Extended Key Use

# Pitfalls to certificate validation

## Not checking the certificate

Failure to check the certificate means your client will communicate with any server using that transport. If you send secrets over the channel, it is trivial for an attacker with the ability to redirect network traffic to read them.

## Trusting more than the server you need to communicate with

The more certificates and certificate authorities you trust, the higher the chance of your transport being intercepted. Limit the parties you trust and review them frequently to ensure you still trust them. 

## Not checking to see if the certificate is expired

## Not checking a certificate revocation list
