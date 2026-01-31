# Field Manual

A fast, grep-first reference of commands and payload primitives for day-to-day security work, labs, and CTFs.

Design goals:
- **One command = one outcome**
- **Outcome > tool**
- **Examples beat explanation**
- **Searchability > hierarchy**
- **No duplicated commands**
- **No invented content** (everything is sourced from raw notes; unclear items are flagged)

---

## Repository Layout

```bash
field-manual/
├── README.md
├── unix/
│ ├── file-discovery.md
│ ├── text-processing.md
│ ├── permissions-and-privesc.md
│ └── shells-and-tty.md
├── networking/
│ ├── curl.md
│ ├── listeners-and-ports.md
│ └── dns-commands.md
├── security/
│ ├── encoding-and-obfuscation.md
│ ├── web-primitives.md
│ ├── xss-payloads.md
│ ├── command-injection.md
│ └── (more as added)
├── tools/
│ ├── ffuf.md
│ ├── gobuster.md
│ ├── feroxbuster.md
│ ├── dig.md
│ ├── finalrecon.md
│ └── recon-frameworks.md
├── reference/
│ ├── http-headers.md
│ ├── http-methods.md
│ ├── http-status-codes.md
│ ├── dns-records.md
│ ├── api-types.md
│ ├── well-known-uris.md
│ ├── posix-signals.md
│ └── wordlists.md
├── qol/
│ ├── aliases.md
│ └── misc-tricks.md
└── _inbox/
├── misc-unfiled.md
└── (things pending review)
```

---

## How to Use (Grep-First)

Set the repo root once:

```bash
export FM="$HOME/field-manual"
Search by outcome (recommended)
```
```bash
rg -n --hidden -S "reverse shell|listener|file transfer" "$FM"
rg -n --hidden -S "suid|world-readable|permissions" "$FM/unix"
rg -n --hidden -S "sqli|sqlmap|INFORMATION_SCHEMA" "$FM/security"
rg -n --hidden -S "xxe|ssrf|ssti" "$FM/security"
Search within a scope
```
```bash
rg -n --hidden -S "ffuf " "$FM/tools"
rg -n --hidden -S "curl -I|--head" "$FM/networking/curl.md"
Find anything that needs verification
```
```bash
rg -n --hidden -S "Review:" "$FM"
Interactive Search (Recommended)
If you use the fmf() helper (ripgrep → fzf → preview → open at line in nvim):
```
```bash
fmf "reverse shell"
fmu "pty.spawn|stty raw"
fmx "SSRF|gopher://|<!ENTITY"
fmi "Review:"
(See your shell config for the fmf()/fmu()/fmn()/fmx() functions.)
```
## Conventions

### Formatting

    - Headings are outcomes
    - Code blocks contain copy/paste-ready commands
    - Variants live under the same outcome heading when they achieve the same thing

### Flags
    - Review: unclear, truncated, or version-sensitive notes
    - Items that don’t fit the current structure land in _inbox/ until sorted

## Workflow for Updates

    1. Drop raw snippets into _inbox/
    2. Deduplicate by searching for similar outcomes:

```bash
rg -n --hidden -S "keyword" "$FM"
```
    3. Move into the correct file and keep one canonical version
    4. Keep anything uncertain flagged with Review instead of guessing

# Disclaimer

**This repository is a personal reference meant for authorized testing, labs, and learning. Only use techniques and tooling where you have explicit permissision.**

