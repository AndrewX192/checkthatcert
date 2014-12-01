# Ruby 

This will check the certificate specified and the local truststore. Sites that have certificates in your trust store such as Google will always verify regardless of the cert specified.

```
require "net/https"
require "uri"
ssltest = Net::HTTP.new("localhost", 4433)
ssltest.use_ssl = true
ssltest.verify_mode = OpenSSL::SSL::VERIFY_PEER
store = OpenSSL::X509::Store.new
store.add_file("cert.pem")
ssltest.cert_store = store
begin 
	response = ssltest.request(Net::HTTP::Get.new("/"))
rescue OpenSSL::SSL::SSLError 
	puts "The certificate did not verify."
else 
	puts "The certificate matches."
end
```
