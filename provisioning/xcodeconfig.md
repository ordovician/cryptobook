# xCode Configuration

Follow these steps to find which provisioning profile a given target is using.

1. Select blue icon representing your project in project navigator (folder icon on left most side).
2. Select your target from the leftmost dropdown menu in view of your selected project icon.
3. Click **Build Settings** tab.
4. Scroll down to the **Code Signing** header
5. Here you can see both **Code Signing Identify** and **Provisioning Profile**

Your code *signing identity* will have to have its corresponding certificate in the selected *provisioning profile*. Remember *code signing identity* is both public and private key while the certificate stored in the *provisioning profile* only contains the public key.
