Wireshark will decrypt WPA2 packets, but this technique doesn't work with WPA3.

The problem I faced is that the settings of router was WPA2/WPA3, that was confirmed by command on my pc "nmcli dev wifi".

The decryption of the first packet capture was not possible, because my phone negotiated WPA3 as a protocol.

That is visible on the screenshot in this folder, please take a look at the line Auth Key Management, where SAE is used, which means that WPA3 is in use.

The router settings had to be changed to WPA2-Personal, in order to force the devices to work with this protocol.

The new packet capture was successfully decrypted by Wireshark.
