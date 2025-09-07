In order to setup Wireshark to decrypt the captured traffic, do the following:
1. Click "Edit" in the top left menu
2. Click "Preferences"
3. Select IEEE 802.11 (the list on the left side of the window)
4. Check box "Enable decryption" (also, depending on your OS and Wireshark version, you might need to Check the boxes: "Assume packets have FCS" and "Ignore the protection bit")
5. Click "Edit" by the "Decryption keys"
6. In the new window under "Key-type" choose "wpa-pwd" and under the "Key" enter: "yourpass:SSID" (it's case sensitive, also space sensitive, there type your password:nameOfYourWifi)
7. Click "Ok"
8. You might need to close the Wireshark and reopen it in order to accept the changes.
