# Cloud Network Traffic Analysis Report — My Solution

For this project, I took the DNS, TCP, HTTP, and TLS findings from my Project 1 capture and matched each one to the cloud security control that would catch or reveal the same activity on AWS or Azure. The idea is simple: what Wireshark shows me on a single machine, a cloud platform should also be able to show me at the network level, just through logs instead of a packet capture.

I didn't stand up a live AWS or Azure environment for this. What I've done is a conceptual translation, showing exactly which service or log type maps to each finding, and why it matters.

## Methodology

I started from my own capture, filtered by `dns`, `tcp`, `http`, and `tls` (see `filters/wireshark-filters.md`), pulled out the behaviour worth flagging, then asked myself: "if this same traffic happened inside a VPC or Azure VNet, what log or control would show it to me?"

## Findings Mapped to Cloud Controls

| What I found on the wire | Cloud equivalent | Why it matters |
|---|---|---|
| DNS query/response pairs, correctly matched by transaction ID, all `NOERROR` | Route 53 Resolver Query Logs (AWS) / Azure Firewall DNS Proxy logs | Plain VPC Flow Logs don't capture DNS content, only the connection. If I actually want to see which domains are being resolved from inside a VPC, I need DNS-specific logging switched on separately. |
| Three ICMP "Port Unreachable" messages mixed into DNS traffic | NSG/VPC Flow Log entries with `REJECT`/`ACTION=DROP` | On its own this is harmless, but a rising count of rejected flows against the same destination is exactly the pattern a Security Group or NSG deny-log would flag as worth a second look. |
| Clean TCP three-way handshake to port 443 | VPC Flow Logs (5-tuple: src/dst IP, port, protocol, action) | A completed, accepted flow to port 443 is the cloud-log version of what I saw frame-by-frame in Wireshark — same story, just summarised instead of packet-level. |
| Plaintext HTTP request/response on port 80 (the `generate_204` connectivity check) | Security Group / NSG egress rule restricting port 80 | Even though this specific request was harmless, allowing unrestricted outbound port 80 is how real data ends up leaving in the clear. I'd lock egress down to only the destinations that genuinely need HTTP. |
| TLS 1.3 handshake with visible SNI (`media-los4-1.cdn.whatsapp.net`) and JA3/JA4 fingerprints | AWS Network Firewall / Azure Firewall Premium (TLS inspection) | Even encrypted, the SNI field is sent in the clear, so a cloud firewall can still allow or block by hostname without decrypting anything. JA3/JA4 hashes are also something I could feed into Azure Sentinel or GuardDuty as threat-intel indicators. |
| TLS 1.3 certificate exchange fully encrypted (unlike TLS 1.2) | Sentinel/GuardDuty behavioural detection instead of payload inspection | Since I can't inspect the certificate in transit anymore, cloud security has to lean more on metadata (SNI, JA3/JA4, connection patterns) rather than content inspection — that's a real shift TLS 1.3 forces on monitoring. |

## Deliverables

- `docs/Cloud-Network-Traffic-Analysis-Report.md` — this report
- `filters/wireshark-filters.md` — the filters I used to isolate each protocol
- `screenshots/` — organised by protocol (`dns/`, `tcp/`, `http/`, `tls/`), empty for now, ready for me to drop my own captures in

## Closing Thought

What this project made clear to me is that packet-level visibility and cloud-log visibility aren't the same thing, and one doesn't automatically give you the other. DNS needs its own logging switched on. TLS 1.3 hides more than TLS 1.2 did, so cloud security has to shift toward metadata like SNI and JA3/JA4 instead of reading the payload. And a lot of what looks like "just background noise" in Wireshark — a port-unreachable message, a plaintext connectivity check — is exactly the kind of thing a Security Group or NSG rule exists to control at scale.
