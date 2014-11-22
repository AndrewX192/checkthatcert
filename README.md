Check That Cert!
=============

Unless you verify who are talking to, having an encrypted channel isn't useful. Not checking the SSL certificate of a remote server you are communicating with allows anyone with control of the network to stand up their own server and certificate, impersonating your server.


# Generating a self signed certificate

````
openssl genrsa -out server.pem 4096
openssl req -new -x509 -key server.pem -out cert.pem -days 30
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
