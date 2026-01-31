# tools/gobuster.md

## Discover virtual hosts (vhost brute force)
    gobuster vhost -u http://example.com/ -w /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt --domain inlanefreight.htb --append-domain
    gobuster vhost -u http://example.com -w hostnames.txt

## Brute-force directories/files (dir mode)
    gobuster dir -u http://example.com -w /path/to/wordlist -t 50 -x php,txt,html
    gobuster dir -u http://example.com -w wordlist.txt

## Brute-force with extensions
    gobuster dir -u http://example.com -w wordlist.txt -x .php,.html

## Filter results by status code
    gobuster dir -u http://example.com -w wordlist.txt -s 200

## Set concurrency (threads)
    gobuster dir -u http://example.com -w wordlist.txt -t 50

## Output results to a file
    gobuster dir -u http://example.com -w wordlist.txt -o results.txt

## Brute-force DNS subdomains (dns mode)
    gobuster dns -d example.com -w subdomains.txt

## Show IPs for discovered subdomains
    gobuster dns -d example.com -w subdomains.txt -i

## Silent mode (only show results)
    gobuster dns -d example.com -w subdomains.txt -z
