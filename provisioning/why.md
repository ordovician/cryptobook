# Why do we need a Provisiong Profile?

Can't we just sign the apps? The reason is that Apple does not want us to be able to distribute the signed apps to any device. That would allow us to circumvent the appstore and Apple's verification that the app is safe for anybody to use. So Apple wants us to restrict the number of devices we can place our apps on and which apps we can place there.

That is what the provisiong profile is for. We make updates to it through a web interface so Apple can sign it and we can download it. Because it is signed by Apple, iOS can trust it's content.

## Example program

This will print out a list of the names of all the people who have a certificate stored in the provisioning profile. Typically a team provisioning profile contains a list of certificates for every developer.

In this example we have extracted the XML part from the provisioning profile and stored in a file named `teamprovisioning.plist`. Otherwise `xpath` will not work, because it can not deal with the binary data prefix in the provisioning profile.

	#!/bin/sh
	for (( i = 1; i <= 16; i++ )); do
		rm cert.pem
		echo -----BEGIN CERTIFICATE----- > cert.pem
		xpath teamprovisioning.plist plist/dict/array/data[$i] | tail -n 34 | head -n 33 >> cert.pem
		echo -----END CERTIFICATE----- >> cert.pem
		openssl x509 -text -in cert.pem | ack Subject
	done
	
## xCode Configuration

Follow these steps to find which provisioning profile a given target is using.

1. Select blue icon representing your project in project navigator (folder icon on left most side).
2. Select your target from the leftmost dropdown menu in view of your selected project icon.
3. Click **Build Settings** tab.
4. Scroll down to the **Code Signing** header
5. Here you can see both **Code Signing Identify** and **Provisioning Profile**

Your code *signing identity* will have to have its corresponding certificate in the selected *provisioning profile*. Remember *code signing identity* is both public and private key while the certificate stored in the *provisioning profile* only contains the public key.

## Getting info about how an app has been signed

*Apple Root CA*, has signed *Apple Worldwide Developer Relations Certification Authority* which has signed certificate *iPhone Distribution: REAKTOR AS*, which has been used to actually sign the executable.

This is valid because the certificate signing chain is no longer than three links. 

	$ codesign -dvvv Systemspill.app 
	Executable=/Users/erikengheim/Library/Developer/Xcode/DerivedData/Systemspill-cadtzgsdfjkesuaazsbldkfdgbua/Build/Products/Debug-iphoneos/Systemspill.app/Systemspill
	Identifier=no.knowit.systemspill
	Format=bundle with Mach-O universal (armv7 (12:11))
	CodeDirectory v=20100 size=8950 flags=0x0(none) hashes=439+5 location=embedded
	Hash type=sha1 size=20
	CDHash=2ee0c12f668b02980e95eb2232944569cd8669bb
	Signature size=4299
	Authority=iPhone Distribution: REAKTOR AS
	Authority=Apple Worldwide Developer Relations Certification Authority
	Authority=Apple Root CA
	Signed Time=18. sep. 2013 10:46:08
	Info.plist entries=31
	Sealed Resources rules=3 files=391
	Internal requirements count=1 size=172
	
This is how the app might look when signed locally. When placed on the appstore the certificate used to sign the executable will be from Apple. So the 3 Authority lines will look like this:

	Authority=Apple iPhone OS Application Signing
	Authority=Apple iPhone Certification Authority
	Authority=Apple Root CA
	
I verified this by copying the `.ipa` package for dragonbox, changed suffix to `.zip` and unpacked it. Then I ran:

	codesign -dvvv DragonBox+\ 1.1.1/Payload/DragonBoxPlus.app/DragonBoxPlus 
	
# Developer Certificate

With the **Keychain Access** application in the ulities folder on your Mac you can easily create public and private key pairs. You can sign an executable with this private key but it won't be considered valid until Apple in the role as *Certiticate Authority* (CA) has signed your public key, thus creating a *secure certificate*. Otherwise there is nobody vouching for your identify.

1. Select your key (not sure if it makes a difference if it is private or public)
2. And then select the menu `Keychain Access > Certificate Assistant > Request Certificater From Certificate Authorith with...`.
3. This uses your public key to create a signing request file on disk.
4. Upload this Apple Developer centre. Apple will then process this request and after some time you can download a **signed** certificate.
5. Double click certificate and add it to your **login keychain**. Why it it needs to be this keychain in particular I don't know.