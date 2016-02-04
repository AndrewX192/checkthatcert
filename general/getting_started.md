# Getting the Certificate of the Remote Server

## Using a Web Browser
The easiest way to retrieve the certificate for a web server using HTTPS is to export it from a web browser.
Aside from being the simplest way to acquire a site's certificate this has the advantage of using the browser's
built-in certificate validation.

The following instructions are for Google Chrome, but the process is very similar in other browsers.
First go to the site in question. Click on the padlock in the address bar and select 'Certificate information' under
the connection tab. Click the 'Details' tab. Click 'Export...' and save the certificate with a name related to the
application, such as 'example.com.pem'


## Using OpenSSL s_client
If it is not possible to use a web browser to get the certificate, OpenSSL's s_client can be used instead. This is
useful for non-http based services. This must be done with care though, as s_client does not perform any certificate
validation, so you will need to verify the certificate manually. A web browser should be favoured where possible.

The following command shows the certificate for https://www.example.com
```
openssl s_client -connect www.example.com:443
```
The certificate starts '-----BEGIN CERTIFICATE-----' and ends with '-----END CERTIFICATE-----'. You can either copy
and paste it from there, including the 'BEGIN' and 'END' lines, or dump it do a file using a command like the following:
```
openssl s_client -connect www.example.com:443 < /dev/null | openssl x509 -outform pem > example.com.pem
```

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
