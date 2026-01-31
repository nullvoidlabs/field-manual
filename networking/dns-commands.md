# networking/dns-commands.md

## Add a local DNS entry to /etc/hosts (append)
    sudo sh -c 'echo "SERVER_IP academy.htb" >> /etc/hosts'
    echo "10.10.11.44 alert.htb" | sudo tee -a /etc/hosts

## Append an additional hostname to an existing /etc/hosts line
    sudo sed -i '/10.10.11.44 alert.htb/ s/$/ statistics.alert.htb/' /etc/hosts # Append host
    sudo sed -i '/94.237.121.185 sql.local/ s#$# subd.sql.local#' /etc/hosts # Append host

## Replace a hostname in /etc/hosts
    sudo sed -i 's#sample.testing$#sample.test#' /etc/hosts # Change just host
    sudo sed -i 's#sample.testing#sample.test#' /etc/hosts # Change just host

## Replace an IP in /etc/hosts
    sudo sed -i 's#^94.237.60.55#94.237.55.43#' /etc/hosts # Change just IP
