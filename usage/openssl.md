# OpenSSL

x509 is a standard for certificates using Certificat Authorities. That differs from say PGP where anybody can sign a certificate. 

Converting between formats. If you have a binary certificate in `DER` format you can convert it to text like this:

	openssl x509 -text -inform DER -in test.realestate.knowit.no.cer  -noout
	
	
# Creating Self Signed Certificates

Create a RSA private key (key based on RSA algorithm by Rivest, Shamir and Adleman):
	
	openssl genrsa -out myselfsigned.key 2048	
	
Then use *myselfsigned.key* to create the self signed certificate:
	
	openssl req -new -x509 -key myselfsigned.key -out myselfsigned.cer -days 365 -subj /CN=www.mysite.com

This creates a *x509* certificate, which expires in 365 days. 


	Certificate:
	    Data:
	        Version: 3 (0x2)
	        Serial Number:
	            a7:b7:5c:95:9f:92:69:62
	        Signature Algorithm: sha1WithRSAEncryption
	        Issuer: CN=www.mysite.com
	        Validity
	            Not Before: Jan  8 09:13:50 2014 GMT
	            Not After : Jan  8 09:13:50 2015 GMT
	        Subject: CN=www.mysite.com
