require "net/https"
require "uri"
ssltest = Net::HTTP.new("localhost", 4433)
ssltest.use_ssl = true
ssltest.verify_mode = OpenSSL::SSL::VERIFY_PEER
store = OpenSSL::X509::Store.new
store.add_file("/Users/jacob/Desktop/junk.pem")
ssltest.cert_store = store
begin 
	response = ssltest.request(Net::HTTP::Get.new("/"))
rescue OpenSSL::SSL::SSLError 
	puts "The cert did not verify"
else 
	puts "The cert verified"
end