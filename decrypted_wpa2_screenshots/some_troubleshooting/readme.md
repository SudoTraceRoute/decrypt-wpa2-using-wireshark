Wireshark will decrypt WPA2 packets, but this technique doesn't work with WPA3.

The settings of router was WPA2/WPA3, that was confirmed by Terminal command: "nmcli dev wifi".

The decryption of the first packet capture was not possible, because my phone negotiated WPA3 as a encryption certificate.

That is visible on the screenshot in this folder, please take a look at the line "Auth Key Management", where SAE is applied, which means that WPA3 is in use.

The router settings had to be changed to WPA2-Personal, in order to force the devices to work with this protocol.

The new packet capture was successfully decrypted by Wireshark.
