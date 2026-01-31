# security/password-attacks.md

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


## Generate username wordlists (username-anarchy)

### Generate usernames from a full name
    username-anarchy Jane Smith

### Use an input file of names
    username-anarchy -i names.txt

### Auto-generate using common names dataset (US)
    username-anarchy -a --country us

### List available username format plugins
    username-anarchy -l

### Use specific format plugins (comma-separated)
    username-anarchy -f format1,format2

### Append email domain suffix
    username-anarchy -@ example.com

### Generate case-insensitive usernames (lowercase)
    username-anarchy --case-insensitive


## Generate password wordlists (CUPP)

### Interactive profile-based generation
    cupp -i

### Generate from a predefined profile file
    cupp -w profiles.txt

### Download popular password lists (e.g., rockyou.txt)
    cupp -l


## Filter wordlists by password policy (grep + regex)

### Minimum length (example: >= 8 chars)
    grep -E '^.{8,}$' wordlist.txt

### At least one uppercase letter
    grep -E '[A-Z]' wordlist.txt

### At least one lowercase letter
    grep -E '[a-z]' wordlist.txt

### At least one digit
    grep -E '[0-9]' wordlist.txt

### At least one special character
⚠️ Review: Quoting/escaping is fragile here; keep as raw source and verify in your shell.
    grep -E '[!@#$%^&*()_+-=[]{};':"\,.<>/?]' wordlist.txt

### Match consecutive repeated characters (use grep -v to exclude)
    grep -E '(.)\1' wordlist.txt

### Exclude common patterns (example: "password", case-insensitive)
    grep -v -i 'password' wordlist.txt

### Exclude words present in a dictionary file
    grep -v -f dictionary.txt wordlist.txt

### Chain multiple requirements (example: >=8 and contains uppercase)
    grep -E '^.{8,}$' wordlist.txt | grep -E '[A-Z]'


## Default credential references (links)
- https://www.cirt.net/passwords
- https://github.com/danielmiessler/SecLists/tree/master/Passwords/Default-Credentials
- https://github.com/scadastrangelove/SCADAPASS/tree/master
