# tools/ffuf.md

## Directory fuzzing
    ffuf -w wordlist.txt:FUZZ -u http://example.com/FUZZ

## Extension fuzzing
    ffuf -w wordlist.txt:FUZZ -u http://example.com/indexFUZZ

## Page fuzzing (path + extension)
    ffuf -w wordlist.txt:FUZZ -u http://example.com/blog/FUZZ.php

## Recursive fuzzing (depth 1, add extensions, verbose)
    ffuf -w wordlist.txt:FUZZ -u http://example.com/FUZZ -recursion -recursion-depth 1 -e .php -v

## Subdomain fuzzing (FUZZ as subdomain)
    ffuf -w wordlist.txt:FUZZ -u https://FUZZ.example.com/

## VHost fuzzing (Host header)
    ffuf -w wordlist.txt:FUZZ -u http://example.com/ -H 'Host: FUZZ.example.com' -fs xxx

## Parameter fuzzing (GET)
    ffuf -w wordlist.txt:FUZZ -u http://example.com/admin/admin.php?FUZZ=key -fs xxx

## Parameter fuzzing (POST)
    ffuf -w wordlist.txt:FUZZ -u http://admin.example.com/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx

## Value fuzzing (POST)
    ffuf -w ids.txt:FUZZ -u http://admin.example.com/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
