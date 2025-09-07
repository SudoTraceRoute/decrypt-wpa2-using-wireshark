# Decrypt-WPA2-using-Wireshark
Capture and decryption of wifi wpa2 packets, EAPOL, ARP, DHCP


# 🔐 Wi-Fi Packet Capture & WPA2 Decryption (with Wireshark)

This project demonstrates how to capture and decrypt WPA2-encrypted Wi-Fi traffic using monitor mode, Wireshark, and a known network passphrase. It includes real-world packet captures, protocol analysis, and troubleshooting notes — including challenges when WPA3 is enabled.

---

## 📦 Contents

- 🖼️ Screenshots (both encrypted and decrypted packet views)
- 📝 Step-by-step WPA2 decryption instructions
- ⚠️ WPA3 troubleshooting and limitations
- 🔍 Protocol breakdown: EAPOL, DHCP, ARP
- 💡 Observations on dropped packets, adapter limits

---

## 🛠️ Setup & Tools Used

- **Wi-Fi Adapter:** WiFi Nation WN-H3 (USB)
- **OS:** Parrot OS (Linux, Debian-based)
- **Phone:** Android device (client)
- **Router:** WPA2/WPA3 mixed mode, SSID: `asdfgh`, Channel: 11
- **Wireshark Version:** 4.0.4

### CLI Tools


- nmcli dev wifi         # Check current Wi-Fi encryption modes

- sudo ip link set wlan0 down

- sudo iw dev wlan0 set type monitor

- sudo ip link set wlan0 down

- sudo iw dev wlan0 set channel 11

(**instead wlan0 use the name of the your's wifi adapter interface**)


**🎯 Objective**

Capture a full WPA2 4-way EAPOL handshake

Decrypt Wi-Fi traffic using Wireshark and known credentials

Analyze decrypted packets: DHCP, ARP, ICMPv6

Investigate why TCP/HTTP/TLS traffic may not be captured or decrypted

Troubleshoot WPA3-related issues


**📸 Capturing the Handshake**

Set adapter to monitor mode and fix to correct channel.

Use Wireshark to start capture.

Force phone to reconnect to Wi-Fi (disconnect → forget network → reconnect).

Generate some traffic by browsing (images, pages, etc.).

Save .pcap file.


**🔓 Decryption in Wireshark**

Open .pcap file.

Go to:
Edit → Preferences → Protocols → IEEE 802.11

Enable: ✅ "Enable decryption"

Click "Edit" next to Decryption Keys.

Add:

Key Type: wpa-pwd

Key: yourpassword:YourSSID
(No wpa-pwd: prefix — just password and SSID separated by colon)

Apply and review decrypted frames.

🧪 Verifying Decryption

You can confirm decryption is working if:

Wireshark identifies ARP, DHCP, ICMPv6, etc.

Example from packet details:
Protocols in frame: radiotap:wlan_radio:wlan:llc:arp

Coloring rules like arp, dhcp, etc. are applied

You see real IP addresses and payloads

Screenshot examples:

📁 screenshots/ folder contains:

EAPOL handshake packets (1–4)

Decrypted DHCP exchange:

Discover → Offer → Request → ACK

Highlighted fields: MAC addresses, timestamps, IPs


**🧱 Protocols Observed**

EAPOL – 4-way WPA2 handshake

DHCP – IP assignment (Discover, Offer, Request, ACK)

ARP – Address resolution

ICMPv6, mDNS, IGMPv3 – Multicast and control protocols

❌ No TCP, HTTP, or TLS packets were decrypted — see reasons below.

🚫 Missing TCP / HTTP / TLS Packets?

Although browsing activity was generated, no TCP or TLS packets were decrypted. Likely reasons:

🧱 USB adapter limitations (dropped high-throughput packets)

📶 Signal loss or interference in monitor mode

❌ Wi-Fi adapter may not handle 802.11n/ac/ax data frames well

🧩 TLS traffic is encrypted end-to-end and often fragmented

This is a hardware limitation, not a decryption failure.

⚠️ Troubleshooting WPA3 Decryption

Wireshark cannot decrypt WPA3 traffic using the password like it can with WPA2.

What happened:

Router was set to WPA2/WPA3 Mixed Mode

Phone negotiated WPA3 using SAE (Simultaneous Authentication of Equals)

Wireshark showed:

Auth Key Management:
  SAE (SHA256)


SAE confirms WPA3 was in use — no passive decryption possible

Solution:

Changed router mode to WPA2-Personal only

Reconnected phone to force WPA2

Captured new handshake

✅ Wireshark successfully decrypted new capture

Why WPA3 Can’t Be Decrypted Like WPA2

WPA3 uses forward secrecy (SAE), which doesn't expose enough key material during handshake

No PSK (pre-shared key) is transmitted or derivable from the handshake

Decryption requires a live MITM attack — not feasible or ethical in typical analysis
