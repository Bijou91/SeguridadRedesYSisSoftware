# Chrono

## Descripción
How to automate tasks to run at intervals on linux servers?
## Solución
### Solución:
```
┌──(kali㉿kali)-[~]
└─$ ssh -p 53484 picoplayer@saturn.picoctf.net
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.8.0-1044-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Last login: Tue Feb 17 03:47:19 2026 from 177.232.4.154
picoplayer@challenge:~$ ls -la
total 16
drwxr-xr-x 1 picoplayer picoplayer   41 Feb 17 03:46 .
drwxr-xr-x 1 root       root         24 Aug  4  2023 ..
-rw------- 1 picoplayer picoplayer   67 Feb 17 03:49 .bash_history
-rw-r--r-- 1 picoplayer picoplayer  220 Feb 25  2020 .bash_logout
-rw-r--r-- 1 picoplayer picoplayer 3771 Feb 25  2020 .bashrc
drwx------ 2 picoplayer picoplayer   34 Feb 17 03:45 .cache
-rw-r--r-- 1 picoplayer picoplayer  807 Feb 25  2020 .profile
picoplayer@challenge:~$ cat /etc/crontab
# picoCTF{Sch3DUL7NG_T45K3_L1NUX_0bb95b71}
```

picoCTF{Sch3DUL7NG_T45K3_L1NUX_0bb95b71}
## Notas
