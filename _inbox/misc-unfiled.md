# _inbox/misc-unfiled.md

⚠️ Review: These entries didn’t fit cleanly into the current canonical file map without adding new files (e.g., `networking/ssh.md`, `unix/mounts.md`, `tools/archive-cracking.md`). Keep here until you decide whether to expand the structure.

## SSH connect using legacy KEX/ciphers (server compatibility)
⚠️ Review: Placeholder text `(their offer)` must be replaced with actual algorithms from the server banner / negotiation output.
    ssh 10.0.0.1 -oKexAlgorithms=+(their offer) -c (their offer)

## Mount an NFS export
⚠️ Review: Replace `{mounted dir}` and `{name}` with real values; requires NFS client support.
    mount -t nfs 10.0.0.1:/{mounted dir} /mnt/{name}

## Crack password-protected ZIP with a dictionary
    fcrackzip -v -u -D -p /usr/share/wordlist/rockyou.txt save.zip
