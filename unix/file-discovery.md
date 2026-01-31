# unix/file-discovery.md

## Find files by name

```bash
sudo find / -name xwiki 2>/dev/null
```

## Find SUID binaries

```bash
find / -perm -4000 -type f 2>/dev/null
```

Notes:
	1- SUID binaries execute with file-owner privileges
	2- Common linux privesc vector
 

