# unix/permissions-and-privesc.md

## List SUID binaries (potential privilege escalation paths)
    find / -perm -4000 -type f 2>/dev/null
    find / -perm -u=s -type f 2>/dev/null

## Find world-readable files (potential sensitive files)
    find / -type f -perm -o+r 2>/dev/null
