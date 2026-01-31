# reference/dns-records.md

## DNS record types (most common)
| Record | Full name | Outcome | Zone file example |
| --- | --- | --- | --- |
| `A` | Address Record | Hostname -> IPv4 address | `www.example.com.` IN A `192.0.2.1` |
| `AAAA` | IPv6 Address Record | Hostname -> IPv6 address | `www.example.com.` IN AAAA `2001:db8:85a3::8a2e:370:7334` |
| `CNAME` | Canonical Name Record | Alias -> canonical hostname | `blog.example.com.` IN CNAME `webserver.example.net.` |
| `MX` | Mail Exchange Record | Mail servers for a domain | `example.com.` IN MX 10 `mail.example.com.` |
| `NS` | Name Server Record | Authoritative name servers for a zone | `example.com.` IN NS `ns1.example.com.` |
| `TXT` | Text Record | Arbitrary text (often verification/policy) | `example.com.` IN TXT `"v=spf1 mx -all"` |
| `SOA` | Start of Authority Record | Zone admin + serial + timers | `example.com.` IN SOA `ns1.example.com. admin.example.com. 2024060301 10800 3600 604800 86400` |
| `SRV` | Service Record | Service -> host:port mapping | `_sip._udp.example.com.` IN SRV 10 5 5060 `sipserver.example.com.` |
| `PTR` | Pointer Record | IP -> hostname (reverse DNS) | `1.2.0.192.in-addr.arpa.` IN PTR `www.example.com.` |

## DNS class field
- `IN` = “Internet” class (common default for modern DNS records). :contentReference[oaicite:0]{index=0}
