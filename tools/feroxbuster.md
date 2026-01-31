# tools/feroxbuster.md

## Basic recursive content discovery with a wordlist
    feroxbuster -u http://example.com -w wordlist.txt

## Include file extensions (as written in source)
    feroxbuster -u http://example.com -w wordlist.txt -x php,html

## Exclude or allow responses by status code 
    feroxbuster -u http://example.com -w wordlist.txt --filter-status 404
    ferocbuster -u http://example.com -w wordlist.txt --status-codes 200

## Set concurrency / threads
    feroxbuster -u http://example.com -w wordlist.txt -t 50

## Set maximum recursion depth
    feroxbuster -u http://example.com -w wordlist.txt --depth 3

## Save output to a file
    feroxbuster -u http://example.com -w wordlist.txt -o results.txt

## Disable recursion
    feroxbuster -u http://example.com -w wordlist.txt --no-recursion

## Follow redirects (as written in source)
⚠️ Review: verify `--url-redirect` flag name for your feroxbuster version.
    feroxbuster -u http://example.com -w wordlist.txt --url-redirect
