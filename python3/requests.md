# Python3 requests

Specify the certificate of the server you want to communicate with in cert.pem. The requests library will only communicate with this server and will ignore the local certificate store.

```
>>> import requests
>>> res = requests.get('https://localhost:4433', verify='cert.pem')
>>> print(res)

```
The following example will catch the error that results if the served certificate does not match the input pem file.

``` python
import requests
try: 
	res = requests.get('https://localhost:4433', verify='cert.pem')   
# Catch exception if SSL certificate does not validate. 
except requests.exceptions.SSLError:
	print "The certificate failed verification."
else:
	print "The certificate passed verification."

```
