# CYSE 425 — Lab 3: IEEE 802.11 Wireless Packet Analysis

![Wireshark](https://img.shields.io/badge/tool-Wireshark-1f6086) ![Protocol](https://img.shields.io/badge/protocol-IEEE%20802.11-21445b) ![Method](https://img.shields.io/badge/method-packet%20analysis-22695d)

Analyzed an **IEEE 802.11 packet capture in Wireshark** to inspect wireless beacon frames, access-point parameters, MAC and IP address relationships, TCP traffic, and the client's disconnection, authentication and association. The lab documents **18 questions** using captured-packet evidence.

**Lab report:** [View the 19-page report PDF (optimized for GitHub)](docs/CYSE425_Lab3_Report.pdf)

## At a glance

| Item | Details |
|---|---|
| Focus | Wireless packet analysis and 802.11 management frames |
| Tool | Wireshark |
| Evidence | 22 screenshots documenting 18 lab questions |
| Protocols | IEEE 802.11, IPv4, TCP and DHCP |
| Observed networks | 30 Munroe St and linksys12, both on channel 6 |

## Assessment Workflow

![Wireshark packet analysis workflow](assets/assessment-flow.svg)

## Evidence Screenshots

All **22 screenshots** from the submitted Lab 3 report are displayed directly below, in report order.

### Beacon frame discovery and access point capabilities

Questions 1–7: SSIDs, channels, beacon timing, MAC addresses and rates.

**01. Beacon frame filtering**

![Screenshot 01: Beacon frame filtering](assets/evidence/01.webp)

*The wlan.fc.type_subtype == 8 display filter isolates IEEE 802.11 beacon frames.*

**02. Identification of the second SSID**

![Screenshot 02: Identification of the second SSID](assets/evidence/02.webp)

*The most frequent SSIDs are 30 Munroe St and linksys12.*

**03. Radio channel for 30 Munroe St**

![Screenshot 03: Radio channel for 30 Munroe St](assets/evidence/03.webp)

*The access point advertises channel 6 at 2437 MHz.*

**04. Radio channel for linksys12**

![Screenshot 04: Radio channel for linksys12](assets/evidence/04.webp)

*The second access point also operates on channel 6.*

**05. Beacon transmission interval**

![Screenshot 05: Beacon transmission interval](assets/evidence/05.webp)

*The beacon interval is 100 time units (TUs), equivalent to 102.4 ms.*

**06. Beacon source MAC address**

![Screenshot 06: Beacon source MAC address](assets/evidence/06.webp)

*The source MAC of the selected beacon is 00:16:b6:f7:1d:51.*

**07. Broadcast destination address**

![Screenshot 07: Broadcast destination address](assets/evidence/07.webp)

*The selected beacon uses ff:ff:ff:ff:ff:ff as the destination address.*

**08. Beacon BSSID**

![Screenshot 08: Beacon BSSID](assets/evidence/08.webp)

*The BSSID matches the transmitting access point: 00:16:b6:f7:1d:51.*

**09. Supported and extended rates**

![Screenshot 09: Supported and extended rates](assets/evidence/09.webp)

*The access point advertises supported and extended rates reaching 54 Mbps.*

### TCP/IP traffic and address interpretation

Questions 8–10: examine TCP SYN and SYN-ACK traffic crossing the wireless link.

**10. TCP SYN packet and link-layer addresses**

![Screenshot 10: TCP SYN packet and link-layer addresses](assets/evidence/10.webp)

*Frame 474 shows a TCP SYN from 192.168.1.109 to 128.119.245.12.*

**11. Destination IPv4 address**

![Screenshot 11: Destination IPv4 address](assets/evidence/11.webp)

*The report identifies 128.119.245.12 as the destination web server gaia.cs.umass.edu.*

**12. TCP SYN-ACK response**

![Screenshot 12: TCP SYN-ACK response](assets/evidence/12.webp)

*Frame 476 illustrates the distinction between IP endpoints and local wireless addresses.*

### Wireless disconnection

Question 11: follow the host disconnecting from the access point.

**13. DHCP Release**

![Screenshot 13: DHCP Release](assets/evidence/13.webp)

*Frame 1733 shows a DHCP Release at approximately 49.5836 seconds.*

**14. 802.11 Deauthentication**

![Screenshot 14: 802.11 Deauthentication](assets/evidence/14.webp)

*Frame 1735 shows a deauthentication frame at approximately 49.6096 seconds.*

### 802.11 authentication exchange

Questions 12–15: authentication method, sequence numbers and acceptance.

**15. Authentication frame selection**

![Screenshot 15: Authentication frame selection](assets/evidence/15.webp)

*Authentication frames are isolated for inspection in Wireshark.*

**16. Open System Authentication request**

![Screenshot 16: Open System Authentication request](assets/evidence/16.webp)

*Frame 2156 requests Open System Authentication (algorithm 0).*

**17. Authentication request sequence**

![Screenshot 17: Authentication request sequence](assets/evidence/17.webp)

*Frame 2156 shows authentication sequence 0x0001.*

**18. Authentication response acceptance**

![Screenshot 18: Authentication response acceptance](assets/evidence/18.webp)

*Frame 2158 reports Successful status 0x0000.*

### Wireless association and data-rate capabilities

Questions 16–18: inspect association requests, responses and advertised rates.

**19. Association request**

![Screenshot 19: Association request](assets/evidence/19.webp)

*Frame 2162 advertises the wireless client's supported data rates.*

**20. Successful association response**

![Screenshot 20: Successful association response](assets/evidence/20.webp)

*Frame 2166 confirms successful association with status 0x0000.*

**21. Client rate capabilities**

![Screenshot 21: Client rate capabilities](assets/evidence/21.webp)

*The client association request includes extended supported rates up to 54 Mbps.*

**22. Access point rate capabilities**

![Screenshot 22: Access point rate capabilities](assets/evidence/22.webp)

*The access point beacon advertises a maximum rate of 54 Mbps.*

## Findings and Evidence

| Finding | Evidence from the report |
|---|---|
| Beacon discovery | The most frequent SSIDs are **30 Munroe St** and **linksys12**, both on channel **6 (2437 MHz)**. |
| Beacon timing | Beacon interval is **100 TUs = 102.4 ms**. |
| Address fields | Beacon source MAC and BSSID: **00:16:b6:f7:1d:51**; broadcast destination: **ff:ff:ff:ff:ff:ff**. |
| Supported rates | Basic rates **1, 2, 5.5, 11 Mbps** and extended rates through **54 Mbps**. |
| TCP traffic | Frames **474** and **476** contain SYN/SYN-ACK traffic between **192.168.1.109** and **128.119.245.12**. |
| Client disconnect | A **DHCP Release** precedes **802.11 Deauthentication**. |
| Authentication | Open System method; request sequence **0x0001**, response **0x0002**, successful status **0x0000**. |
| Association | The access point reports successful association in Frame **2166**; fastest reported supported rate is **54 Mbps**. |

## What This Project Demonstrates

- Applied Wireshark display filters to investigate 802.11 management frames.
- Identified SSIDs, access-point channels, beacon intervals, BSSIDs and data rates.
- Distinguished local link-layer MAC addresses from network-layer IP addresses.
- Traced DHCP Release and Deauthentication during a client disconnect.
- Interpreted Open System Authentication and Association Request/Response exchanges.
