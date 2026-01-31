# security/encoding-and-obfuscation.md

## Base64 encode (string -> b64)
    echo hackme | base64

## Base64 decode (b64 -> string)
    echo ENCODED_B64 | base64 -d

## Hex encode (string -> hex)
    echo hackme | xxd -p

## Hex decode (hex -> string)
    echo ENCODED_HEX | xxd -p -r

## ROT13 encode (string -> rot13)
    echo hackme | tr 'A-Za-z' 'N-ZA-Mn-za-m'

## ROT13 decode (rot13 -> string)
    echo ENCODED_ROT13 | tr 'A-Za-z' 'N-ZA-Mn-za-m'
