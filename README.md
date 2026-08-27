# Network Traffic Flow with Wireshark for Beginners

![Wireshark](https://img.shields.io/badge/Tool-Wireshark-1679A7?logo=wireshark&logoColor=white)
![Kali Linux](https://img.shields.io/badge/OS-Kali%20Linux-557C94?logo=kalilinux&logoColor=white)
![Windows](https://img.shields.io/badge/OS-Windows%2011-0078D6?logo=windows&logoColor=white)
![Cloud](https://img.shields.io/badge/Cloud-AWS%20%7C%20Azure-blueviolet?logo=cloudflare&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-green)

This repo is where I practice reading raw network traffic with Wireshark and turning what I find into actual security understanding — starting from DNS, TCP, HTTP, and TLS packets, and ending with cloud security controls.

Captures were taken from kali Linux v 4.6.6

## Projects

| # | Assignment | My Solution |
|---|---|---|
| 1 | [Analyzing DNS, TCP, HTTP & TLS Traffic with Wireshark](Project-1-Analyzing-DNS-TCP-HTTP-TLS-Traffic-with-Wireshark.md) | [My Solution](Project-1-Analyzing-DNS-TCP-HTTP-TLS-Traffic-with-Wireshark/Project-1-Analyzing-DNS-TCP-HTTP-TLS-Traffic-with-Wireshark.md) |
| 2 | [Translate Protocol Findings Into Cloud Security Controls](Project-2-Translate-Protocol-Findings-Into-Cloud-Security-Controls.md) | [My Solution](Project-2-Translate-Protocol-Findings-Into-Cloud-Security-Controls/Cloud-Network-Traffic-Analysis-Report.md) |

**Project 1** covers the basics — capturing traffic, filtering by protocol, and understanding what a DNS lookup, a TCP handshake, an HTTP request, and a TLS handshake actually look like at the packet level.

**Project 2** builds on that by taking those same findings and mapping them to real cloud security controls — AWS VPC Flow Logs, Security Groups, Azure NSGs — so packet-level visibility connects to something I'd actually use in a cloud environment.

## Repo Structure

```
├── Project-1-Analyzing-DNS-TCP-HTTP-TLS-Traffic-with-Wireshark.md      # assignment brief
├── Project-1-Analyzing-DNS-TCP-HTTP-TLS-Traffic-with-Wireshark/
│   └── Project-1-Analyzing-DNS-TCP-HTTP-TLS-Traffic-with-Wireshark.md  # my solution
├── Project-2-Translate-Protocol-Findings-Into-Cloud-Security-Controls.md   # assignment brief
├── Project-2-Translate-Protocol-Findings-Into-Cloud-Security-Controls/
│   ├── Cloud-Network-Traffic-Analysis-Report.md                        # my solution
│   └── wireshark-filters.md                                            # filters used
├── images/                     # screenshots, by protocol
│   ├── dns_analysis/
│   │   ├── dns_query.png
│   │   ├── dns_response.png
│   │   ├── dns_traffic.png
│   │   └── unfiltered_capture.png
│   ├── tcp_analysis/
│   │   ├── tcp_syn.png
│   │   ├── tcp_syn_ack.png
│   │   ├── tcp_ack.png
│   │   ├── tcp_stream.png
│   │   ├── tcp_traffic.png
│   │   └── unfiltered_capture.png
│   ├── http_analysis/
│   │   ├── http_get.png
│   │   └── http_response.png
│   └── tls_analysis/
│       ├── tls_client_hello.png
│       ├── tls_server_hello.png
│       ├── tls_encrypted_app_data.png
│       └── tls_traffic_filter.png
├── capture.pcap                 # raw capture
├── output2.pcap                 # raw capture, second environment
└── README.md
```

## Tools I Used

- **Wireshark** — packet capture and protocol analysis
- **Kali Linux** — capture environments
- **Browser / curl / ping** — generating traffic to capture
- **AWS & Azure concepts** — VPC Flow Logs, Security Groups, NSGs, Sentinel (for Project 2's mapping)

## About

I put this together to build real, hands-on comfort with Wireshark instead of just reading about protocols — DNS, TCP, HTTP, and TLS make a lot more sense once you've actually watched them happen frame by frame, across two different operating systems.

## License

This project is licensed under the [MIT License](LICENSE).

**COURTESY** 
Mr. Micheal Emeka (M.E.Ns) at BoycodeAfrica Cohort 5.0
