The first packet capture could not be decrypted because the phone negotiated a WPA3 connection using SAE (Simultaneous Authentication of Equals), the key exchange method used by WPA3.

You can verify this in the screenshot provided in this folder — look for the line labeled "Auth Key Management", where SAE is listed. This indicates that WPA3 was in use, and thus the standard WPA2 decryption method would not apply.

To fix this, the router settings were changed to WPA2-Personal only, forcing all devices to use WPA2.

After this change, a new packet capture was made — and Wireshark successfully decrypted it using the WPA2 4-way handshake and the correct password.



Why WPA3 decryption fails:

WPA3 uses forward secrecy and a more secure key exchange method (SAE) that does not transmit any information derived from the password during the handshake. This means:

Even if you know the correct passphrase, Wireshark cannot decrypt WPA3 traffic unless you perform a live man-in-the-middle attack (which is much more advanced and unethical without permission).

The 4-way handshake in WPA3 is cryptographically different and doesn't expose enough information for passive decryption.

WPA3 does not support pre-shared key (PSK) decryption like WPA2.
