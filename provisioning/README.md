# Provisioning Profile

A provisioning profile is **NOT** for signing applications. During development applications are signed with the private key in *Code Signing Identity* (specified in target build settings). When the iOS kernel encounters a signed app, it checks with the installed provisioning profiles whether:

1. Has the app been signed with a private key, which has a corresponding certificate (public key) in one of the provisioning profiles?
2. Is the **ID** of the app in the provisiong profile?
3. Are we on a *device* listed in the provisoning profile containing said certificate and *app id*?

If all of these criteria are fullfilled we can run the application.

Provisioning profiles can be used to run apps in different ways:

1. Run on device thru xCode (iOS Team Provisioning Profile)
2. Ad Hoc distribution
3. App Store
4. Enterprise build for In-House distribution

The provisioning profile is a PKCS#7 signed plist, signed by Apple. Apple works as the Certificate Authority (CA). A plist is a dictionary in XML form. Under the key `DeveloperCertificates` the developer certificate is stored in base64 encoding.

	<key>DeveloperCertificates</key>
	<array>
		<data>
		MIIFeTCCBGGgAwIBA...
		</data>
	</array>
	
Copy data into a file with ending `.pem` like this:
	
	-----BEGIN CERTIFICATE-----
	MIIFeTCCBGGgAwIBA...
	-----END CERTIFICATE-----
	
To the developer certificate stored in a file on PEM format (Privacy Enhanched Email). Inspect content of certificate with:

	$ openssl x509 -text -in mycertificate.pem
	
Apple and iOS use this certificate to verify that code has been signed by appropriate developer.

## Types of Provisioning Profiles

A **team provisioning profile** allows any of the team members to sign an app and run it on any of the devices of the team members. Bob can sign an app an run it on Alice's iOS device as long as they both use the same *team provisioning profile*.
