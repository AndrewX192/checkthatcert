# Getting the Certificate of the Remote Server

OpenSSL's s_client can be used to display the certificate of a server, however this must done with care, as s_client does not perform any certificate validation. Instead, a web browser should be used to connect to the server and save the certificate.
````

````

# Testing
If you want to test if an HTTPS client is performing validation you can use the examples of broken TLS that should be rejected on https://badssl.com/

For example the following call is correctly rejected because the requested domain does not match the certificate:
```
user@localhost> curl https://wrong.host.badssl.com/
curl: (51) SSL: no alternative certificate subject name matches target host name 'wrong.host.badssl.com'
```

An HTTPS client that does not reject requests to the examples of broken TLS on that site is not performing validation correctly.

# Certificate File Formats

# Openssl Utiltiies
