# wget

Specify the certificate of the server you want to communicate with in cert.pem

## This trusts the certificate, but does not override the certstore.

````
$ wget --ca-certificate cert.pem https://localhost:4433
````

