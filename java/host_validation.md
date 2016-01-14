# Host Validation
At times you may need to supply an instance of javax.net.ssl.HostnameVerifier to a library which is making TLS/SSL connections.
A common approach is to provide a custom implementation which simply returns 'true', however this is very dangerous
as it removes all protection against man in the middle attacks.

The rules for hostname verification are actually quite complicated, so implementing your own HostnameVerifier is not recommended.
The safer option is to make use of an existing, good implementation. For example, version 4 of Apache HTTP Client
comes with a suitable hostname verifier: org.apache.http.conn.ssl.DefaultHostnameVerifier

