The first packet capture could not be decrypted because the phone negotiated a WPA3 connection using SAE (Simultaneous Authentication of Equals), the key exchange method used by WPA3.

You can verify this in the screenshot provided in this folder — look for the line labeled "Auth Key Management", where SAE is listed. This indicates that WPA3 was in use, and thus the standard WPA2 decryption method would not apply.

To fix this, the router settings were changed to WPA2-Personal only, forcing all devices to use WPA2.

After this change, a new packet capture was made — and Wireshark successfully decrypted it using the WPA2 4-way handshake and the correct password.
