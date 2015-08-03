# OpenSSL s_client

s_client is a SSL/TLS command line client provided by OpenSSL.

# Problems

Users of s_client will run into a number of issues getting certificate validation to work. This client should probably be rewritten while trying to preserve as much of the original functionality as possible.

## Issuer verification

OpenSSL does not perform issuer verification by default. Providing a list of certificate authorities to s_client does not resolve this issue as OpenSSL does not abort the connection if verification fails.

## Hostname verification
 
OpenSSL does not do any hostname verification. Even if the issuer is verified, anyone who can issue certificates with the trusted certificate authority will be able to present a trusted certificate to the client.

## Verify functionality does not close the connection

By default, the -verify method does not abort the connection. This means that if a caller does not explicitly check the output of s_client before transmitting or accepting data from s_client the application will be subject to MiTM. This is actually a known bug in s_client:

````
BUGS
       Because this program has a lot of options and also because some of the techniques used are rather old, the C source of s_client is rather hard to read and not a model of how things should be done. A
       typical SSL client program would be much simpler.

       The -verify option should really exit if the server verification fails.
````

