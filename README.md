Check That Cert!
=============

Unless you verify who are talking to, having an encrypted channel isn't useful. Not checking the SSL certificate of a remote server you are communicating with allows anyone wuth control of the network to stand up their own server and certificate, impersonating your server.


# Generating a self signed certificate

````
openssl genrsa -out privkey.pem 4096
openssl req -new -x509 -key server.pem -out cacert.pem -days 30
````
