
# How to set up a ssh server
This tutorial was tested on debian 

# Default port of ssh
Default port of ssh is 22

Install openssh-server
~~~bash
apt install openssh-server
~~~


There are some related tools of ssh that can be util for you. 

* net-tools package providing netstat command that help you to verify if ssh is running. You can verify status with follow command:

~~~bash
netstat -tulpn | grep :22 # if output is empty, ssh server not running
~~~
* iptables package it's firewall tool that follow you enable specific ports (output, input or both)

~~~bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT # accept input traffic in 22 port
iptables -A OUTPUT -p tcp --dport 22 -j ACCEPT # accept output traffic in 22 port
~~~

## How to start sshd service

With systemd
~~~bash
systemctl start ssh
~~~
or
~~~bash
/etc/init.d/ssh start # this command also accept stop, reload, force-reload, restart, try-restart and status
~~~

# Accept Password authentication

Sometimes password authentication is disabled. If you want enable password authentication you must have to uncomment "PasswordAuthentication yes" in /etc/ssh/ssh_config file. On the other hand, if you want authenticate with root user (that's not recommended) but, it's possible if you uncomment or add "PermitRootLogin yes" in /etc/ssh/sshd_config file

Remember restart ssh service if you do any changes.

# Public Key based authentication
Ensure you ssh server has enabled public key authentication. For enable this feature, a
dd or uncomment "PubKeyAuthentication yes". 


## create key-pair authentication

~~~bash
ssh-keygen -f <key_name> # -f flag is optional
~~~

After key-pair has been created, key-pair must be copy on server thqt you want to authenticate (public key only). The command for copy public key is:

~~~bash
ssh-copy-id -i <public_key_path>
~~~

After that, you can be authenticate in remote server without password

