# networking/curl.md

## Fetch response headers only (HEAD)
    curl -I inlanefreight.com
    curl --head inlanefreight.com

## HTTP GET request
    curl http://SERVER_IP:PORT/

## HTTP POST request
    curl -s http://SERVER_IP:PORT/ -X POST

## HTTP POST request with form data
    curl -s http://SERVER_IP:PORT/ -X POST -d "param1=sample"

## HTTP POST with explicit content-type header (form-urlencoded)
    curl http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=key' -H 'Content-Type: application/x-www-form-urlencoded'

## Enumerate subdomains via crt.sh JSON (wildcard query)
    curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u

## Filter crt.sh JSON results by substring (example: contains "dev")
    curl -s "https://crt.sh/?q=facebook.com&output=json" | jq -r '.[] | select(.name_value | contains("dev")) | .name_value' | sort -u
