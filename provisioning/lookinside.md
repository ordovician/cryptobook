# What does a provisioning profile look like

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
