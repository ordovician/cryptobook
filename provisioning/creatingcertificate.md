# Developer Certificate

With the **Keychain Access** application in the ulities folder on your Mac you can easily create public and private key pairs. You can sign an executable with this private key but it won't be considered valid until Apple in the role as *Certiticate Authority* (CA) has signed your public key, thus creating a *secure certificate*. Otherwise there is nobody vouching for your identify.

1. Select your key (not sure if it makes a difference if it is private or public)
2. And then select the menu `Keychain Access > Certificate Assistant > Request Certificater From Certificate Authorith with...`.
3. This uses your public key to create a signing request file on disk.
4. Upload this Apple Developer centre. Apple will then process this request and after some time you can download a **signed** certificate.
5. Double click certificate and add it to your **login keychain**. Why it it needs to be this keychain in particular I don't know.