Check That Cert!
=============

Unless you verify who are talking to, having an encrypted channel isn't useful. Not checking the SSL certificate of a remote server you are communicating with allows anyone with control of the network to stand up their own server and certificate, impersonating your server.


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

## Issuer

## Valid from-to timestamps

## Extended Key Use
