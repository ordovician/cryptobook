# Getting info about how an app has been signed

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
