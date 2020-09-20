---
layout: post
title:  "Wireguard Setup"
date:   2020-09-20T14:25:52-05:00
author: SASIDHAR
categories: archi3
permalink : /wireguard
cover : "/assets/wolf1.png"

---

# This blogpost describes how to setup wireguard between a server and a client.

###  In this I am not explaining how the commands in configuration file works, read wireguard official documentation for details. I will put the link below.

## SERVER SETUP

### Install wireguard
```sh
sudo apt install wireguard -y
```

### Generate key pairs
```sh
umask 077
wg genkey | tee privatekey | wg pubkey > publickey
```

### Server Config
```sh
[Interface]
PrivateKey = <Private Key>
Address = 10.0.0.1/24, fd86:ea04:1115::1/64 # we can use ((2**(32-24))-2) ip addresses
ListenPort = 51820
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE; ip6tables -A FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE  # here change eth0 to your own interface
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE; ip6tables -D FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
SaveConfig = true
```

### Firewall Port

```sh
Allow port 51820 to public. (ufw or firewalld)
```

### Start wireguard service on server ( remember before making any changes set the interface down)
```sh
sudo wg-quick up wg0  #wg-quick is convinient and easy
```

### To enable autorestart on reboot
```sh
sudo systemctl enable wg-quick@wg0
```
#### Brief output
```sh
sudo wg show
```

## Client setup


### Install wireguard
```sh
sudo apt install wireguard -y
```

### Generate key pairs
```sh
umask 077
wg genkey | tee privatekey | wg pubkey > publickey
```

### Server Config (/etc/wireguard/wg0.conf)
```sh
[Interface]
PrivateKey = <Private Key>
Address = 10.0.0.2/24, fd86:ea04:1115::5/64
ListenPort = 51820
SaveConfig = true

[Peer]
PublicKey = <Server Public key>
Endpoint = <Server Public IP>:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 30
```

### Start wireguard
```sh
sudo wg-quick up wg0
```
### To enable autorestart on reboot
```sh
sudo systemctl enable wg-quick@wg0
```
#### Brief output
```sh
sudo wg show
```



## Go back to server, and do this.

```sh
sudo wg set wg0 peer <Client Public Key> endpoint <Client IP address>:51820 allowed-ips 10.0.0.2/24
```
Start the wireguard service now.

#### Test the connection
> 'ping 10.0.0.2' from server and 'ping 10.0.0.1' from client

### Finally do this on server to forward incoming connections on wireguard interface and send them to other interfaces.

```sh
sysctl sysctl -w net.ipv4.ip_forward=0
```

# Links

[Wireguard Documentstion](https://www.wireguard.com/quickstart/)









