# tools/dig.md

## Basic DNS lookup (A record default)
    dig domain.com

## Query specific record types
    dig domain.com A
    dig domain.com AAAA
    dig domain.com MX
    dig domain.com NS
    dig domain.com TXT
    dig domain.com CNAME
    dig domain.com SOA

## Query a specific DNS server
    dig @1.1.1.1 domain.com

## Trace full DNS resolution path
    dig +trace domain.com

## Reverse DNS lookup (PTR)
    dig -x 192.168.1.1

## Short / minimal output
    dig +short domain.com
    dig +noall +answer domain.com

## Zone transfer (AXFR) attempt (if allowed)
    dig @ns1.example.com example.com axfr

## ANY query (often ignored by DNS servers)
    dig domain.com ANY
