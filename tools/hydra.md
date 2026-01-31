# tools/hydra.md

## Brute-force FTP login (single username, password list)
    hydra -l admin -P /path/to/password_list.txt ftp://192.168.1.100

## Brute-force SSH login (single username, password list)
    hydra -l root -P /path/to/password_list.txt ssh://192.168.1.100

## Brute-force HTTP login form (POST)
    hydra -l admin -P /path/to/password_list.txt 127.0.0.1 http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
