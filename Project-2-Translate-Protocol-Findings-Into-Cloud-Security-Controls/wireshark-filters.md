# Wireshark Filters Used

| Filter | Purpose |
|---|---|
| `dns` | Isolate DNS queries and responses |
| `tcp` | Isolate TCP segments, including the three-way handshake |
| `http` | Isolate plaintext HTTP requests and responses |
| `tls` | Isolate TLS handshake and encrypted application data |
| `icmp` | Check for ICMP errors (e.g. Destination Unreachable) interleaved with other traffic |
