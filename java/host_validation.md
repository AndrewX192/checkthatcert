# Host Validation
At times you may need to supply an instance of javax.net.ssl.HostnameVerifier to a library which is making TLS/SSL connections. A common bad practice is to provide a custom implementation which does not actually perform any host validation, and simply returns 'true'. If the client software does not verify hostnames a man in the middle attacker could present the client with a certificate for a different domain that they control. A well behaved client should reject any certificate that is not for the requested host.

The rules for hostname verification are actually quite complicated, so implementing your own HostnameVerifier is not recommended.
The safer option is to make use of an existing, good implementation. For example, version 4 of Apache HTTP Client
comes with a suitable hostname verifier: org.apache.http.conn.ssl.DefaultHostnameVerifier

