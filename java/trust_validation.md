# How to handle untrusted certificates
One common problem you may come across is that the server presents a certificate that is not trusted by the Java.
This will manifest itself with an error like the following:
```
sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
```


If you know the certificate to be trusted, for example if it is a self signed certificate that you have created,
you can instruct your application to explicitly trust this certificate. This is much safer than disabling trust verification,
and is also technically simpler.

The steps to trust a certificate are:

### 1. Acquire the certificate
See checkthatcert/general/getting_started.md for details on how to do this.

### 2. Add it to a key store
The following command will create a new key store and import the downloaded certificate.
This uses the 'keytool' application, which is bundled with the JRE.
```
keytool -import -alias example.com -file example.com.pem -keystore keystore.jks
```
When creating a new keystore you will be prompted to create a password.
For existing keystores you will be prompted to enter the password.
Keytool will allow you to read a keystore without the password, but requires the password to alter a keystore.

### 3. Instruct the application to use that trust store
To use this keystore in your application run it with the following VM option:
```
-Djavax.net.ssl.trustStore=keystore.jks
```

### How NOT to handle untrusted certificates
The dangerous approach to handling untrusted certificates is to not perform trust validation at all,
which can be done by implementing javax.net.ssl.TrustManager. Sometimes people do this with the intention of only
skipping validation while testing, however as it involves changing code it then ends up in production too.
As it does not leave anything obviously broken this kind of change can go unnoticed quite easily,
but it will leave the application completely unprotected against man in the middle attacks.