# tools/hashcat.md

## Basic syntax
    hashcat -m <hash_mode> -a <attack_mode> <hash_file> <wordlist_or_mask>

## Show help / lookup modes
    hashcat -h
    hashcat --help | grep -i <keyword>        # e.g. md5, ntlm, office, network
    hashcat --example-hashes -m <hash_mode>

## Benchmark
    hashcat -b
    hashcat -b -m <hash_mode>

## Sessions
    hashcat --session <name>
    hashcat --restore

## Output management
    hashcat --show
    hashcat --left
    hashcat -o cracked.txt
    hashcat --remove
    hashcat --username
    hashcat --potfile-disable

## Attack modes (`-a`)
| Mode | Outcome |
| --- | --- |
| 0 | Straight / Dictionary |
| 1 | Combination (dict + dict) |
| 3 | Brute force (mask) |
| 6 | Hybrid (dict + mask) |
| 7 | Hybrid (mask + dict) |

## Character sets (masks)
| Mask | Meaning |
| --- | --- |
| `?l` | lowercase |
| `?u` | uppercase |
| `?d` | digits |
| `?h` | hex (lower) |
| `?H` | hex (upper) |
| `?s` | symbols |
| `?a` | all printable |
| `?b` | all bytes (0x00–0xff) |

## Devices
    hashcat -I           # list OpenCL devices
    hashcat -D 1         # CPU
    hashcat -D 2         # GPU
    hashcat -d <id>      # specific device

## Incremental brute force
    hashcat -a 3 -i hashes.txt ?a?a?a?a?a?a
    hashcat --increment-min 6 --increment-max 8

---

## Common hash modes (high-signal)

### Windows / AD
| Hash | Mode |
| --- | --- |
| NTLM | 1000 |
| NetNTLMv1 | 5500 |
| NetNTLMv2 | 5600 |
| DCC / MSCACHE v1 | 1100 |
| DCC2 / MSCACHE v2 | 2100 |
| LM | 3000 |

### Raw
| Hash | Mode |
| --- | --- |
| MD5 | 0 |
| MD4 | 900 |
| SHA1 | 100 |
| SHA256 | 1400 |
| SHA512 | 1700 |

### Network / Auth
| Hash | Mode |
| --- | --- |
| WPA/WPA2 | 2500 |
| WPA PMK | 2501 |
| Kerberos AS-REQ | 7500 |
| Kerberos TGS-REP | 13100 |

### Databases / CMS (examples)
| Hash | Mode |
| --- | --- |
| MySQL5 | 300 |
| PostgreSQL | 12 |
| WordPress (MD5) | 400 |
| Drupal7 | 7900 |

Review: This is a curated subset. Full authoritative list is extensive.

---

## Common attacks (examples)

### Dictionary (MD5)
    hashcat -m 0 -a 0 hashes.txt rockyou.txt

### Dictionary + rules
    hashcat -m 0 -a 0 hashes.txt wordlist.txt -r rules/best64.rule

### Brute force (7 chars, all printable)
    hashcat -m 0 -a 3 hashes.txt ?a?a?a?a?a?a?a

### Hybrid (dict + 2 chars)
    hashcat -m 100 -a 6 hashes.txt wordlist.txt ?a?a

### Combination attack
    hashcat -m 0 -a 1 hashes.txt dict1.txt dict2.txt

### Kerberoast (wordlist)
    hashcat -m 13100 -a 0 --session crackin1 hashes.txt wordlist.txt -o output.pot

---

## Utilities (hashcat-utils)

### Convert WPA capture
    cap2hccapx.bin input.pcap output.hccapx [essid]

### Calculate keyspace for a mask
    keyspace.bin ?a?a?a?a?a

---

## Known empty hashes
| Type | Value |
| --- | --- |
| LM | aad3b435b51404eeaad3b435b51404ee |
| NTLM | 31d6cfe0d16ae931b73c59d7e0c089c0 |

---

## Notes
- Prefer **wordlists + rules** over raw brute force.
- Mask size grows exponentially (`?a` is expensive).
- Use sessions for long-running jobs.

Source: Hashcat Cheat Sheet v2018.1b (Black Hills InfoSec) 
