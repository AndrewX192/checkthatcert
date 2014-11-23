# Python3 requests

Specify the certificate of the server you want to communicate with in cert.pem. cURL will only communicate with this server and will ignore the local certificate store.

````
>>> import requests
>>> res = requests.get('https://localhost:4433', verify='cert.pem')
>>> print(res)

````

