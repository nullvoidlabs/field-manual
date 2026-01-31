# tools/recon-frameworks.md

## Nikto: identify web server software / common misconfig
### Basic scan
    nikto -host http://[target-IP]

### Software identification modules only
    nikto -h inlanefreight.com -Tuning b

## WAF detection (wafw00f)
### Install (pip)
    pip3 install git+https://github.com/EnableSecurity/wafw00f

 No usage commands for `wafw00f` are curently present.

## Nmap: network discovery, port scanning, service/version detection
### Scan syntax (template)
    nmap [flags] target

### Host discovery (ping sweep)
    nmap -sn [IP-range]

### Fast scan (top ports)
    nmap -T4 -F [target]

### Full TCP scan (all ports, SYN)
    nmap -p- -T4 -sS [target-IP]

### UDP scan (common ports)
    nmap -sU -p 53,161,137 [target-IP]

### Aggressive scan (OS + version + scripts + traceroute)
    nmap -A -p- [target]

### Service/version detection
    nmap -sV

### OS detection
    nmap -O

### Save output (all major formats)
    nmap -sS -p 80,443 [target] -oA scan_results

### Use NSE vuln category (service-based checks)
    nmap -sV --script vuln [target]

### Run a specific NSE script
    nmap --script=smb2-security-mode.nse -p445 10.0.0.1/24 -Pn

### Fragment packets (evasion / filtering tests)
    nmap -sS -f [target]

## SMB enumeration
### List shares
    smbclient -L [target-IP]
    smbclient -L \\10.0.0.1\

### Connect to a share
    smbclient \\10.0.0.1\NAME$

## Exploit database lookup
    searchsploit [service-name or version]

## Recon checklists (raw notes)
    EyeWitness
    Aquatone
    masscan
