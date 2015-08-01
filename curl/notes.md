# cURL

Specify the certificate of the server you want to communicate with in cert.pem. cURL will only communicate with this server and will ignore the local certificate store.

````
$ curl https://localhost:4433/index.html --cacert cert.pem
````

## What's been tested

* Hostname verification
