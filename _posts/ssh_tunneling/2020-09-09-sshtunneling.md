---
layout : post
title : "SSH TUNNELING"
date : 2020-09-09 07:45:36
author : Sasidhar
categories : ssh_tunneling
tags : videos linux ssh tunnels
---

Port forwarding via SSH (SSH tunneling) creates a secure connection between a local computer and a remote machine through which services can be relayed. Because the connection is encrypted, SSH tunneling is useful for transmitting information that uses an unencrypted protocol, such as IMAP, VNC, or IRC. 

# There are total 3 types of port forwarding we can do. They are : 
    * Local Port Forwarding
    * Remote Port Forwarding
    * Dynamic Port Forwarding

## Local Port Forwarding

In this type of port forwarding, let us assume you are at school and your school firewall blocks access to a specific website i.e., blocks the port. ( 80 in common). Then you can forward the port via ssh to remote server and then to destination server.

This is super useful if you want to connect to your remote database server but you dont want to open database ports on remote database server to public. You can create a tunnel and perform ssh local port forwarding.

Another perk is if the end connection is not secure , you can use this to securely access the remote site.

For example, say you wanted to connect from your laptop to http://www.ubuntuforums.org using an SSH tunnel. You would use source port number 8080 (the alternate http port), destination port 80 (the http port), and destination server www.ubuntuforums.org

```sh
ssh -L 8080:www.ubuntuforums.org:80 <host>
```

Now you can access the website 'www.ubuntuformums.org' at localhost:8000

Another example is 

![](/assets/localportforwarding1.png)

In the image above, the blue host cannot reach http://192.168.0.3 but can ssh to 192.168.0.2. The following ssh command executed on the blue host will allow the blue host to reach the red host.
```sh
ssh -L 8080:192.168.0.3:80 reduser@192.168.0.2
```
Now the blue host can open a browser, and go to http://localhost:8080 and be presented with the webpage hosted on 192.168.0.3.

One more example where the ssh server and the destination server are same is :

![](/assets/localportforwarding2.png)

In the image above, the blue host wants to connect to the red host on port 80 but there’s a firewall in between which is denying this. Because the blue host can ssh to the red host, we can create a local port forwarding ssh tunnel to access that port.
The command on the blue host is:

```sh
ssh -L 8080:192.168.0.2:80 reduser@192.168.0.2
```
Now when the blue host opens a browser and goes to http://localhost:8080 they will be able to see whatever the red server has at port 80.


## Remote Port Fowarding

Here , there can be 2 examples too. One is if you want to make your home development server (which is generally on localhost) to be accessible to people outside world. 

Lets say you are 'A' and your friend is 'B'. You want to flask development server on your machine to be accessed by your friend 'B'. But he cannot as yours is a localhost. Then you can forward your remote port say 8080 on your ssh server on cloud to your system ('A').
You can do this using following : 

```sh
ssh -R <remotesshport>:<remote_ssh_server_ip>:<your_local_port> username@<remote_ssh_server>
```
Now your friend can access your development server at http://<remote_ssh_server>:<remotesssport>

Another example is :
In this scenario we are creating a reverse ssh tunnel. Here we can initiate an ssh tunnel in one direction, then use that tunnel to create an ssh tunnel back the other way.

![](/assets/remoteportforwarding1.png)

We are on the green host and want to ssh to the blue host. However, the firewall blocks this connection directly. Because the blue host can ssh to the green host, we can connect using that, and when the green host wants to ssh back to the blue host, it can ride along this previously established tunnel.

Blue host initiates ssh tunnel like this:
```sh
ssh -R 2222:localhost:22 greenuser@192.168.0.3
```

This opens port 2222 on the green host, which is then port forwarding that to port 22 on the blue host. So if the green host were to ssh to itself on port 2222 it would then reach the blue host.

Green host can now ssh to blue host like this:
```sh
ssh -p 2222 blueuser@localhost
```
### Using the N-Option
When using ssh, you can specify the -N flag which tells ssh you don’t need to send any commands over the ssh connection when it’s established. This option is often used when making tunnels since often we don’t need to actually get a prompt.
