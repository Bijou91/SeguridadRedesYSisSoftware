# Commitment Issues

## Descripción
I accidentally wrote the flag down. Good thing I deleted it!
## Solución
### Solución:
```
Bijou91-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c_titan/138/challenge.zip
--2026-02-17 04:15:03--  https://artifacts.picoctf.net/c_titan/138/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.170.131.72, 3.170.131.18, 3.170.131.77, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.170.131.72|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 19199 (19K) [application/octet-stream]
Saving to: 'challenge.zip'

challenge.zip                                   100%[======================================================================================================>]  18.75K  --.-KB/s    in 0.006s  

2026-02-17 04:15:03 (3.21 MB/s) - 'challenge.zip' saved [19199/19199]

Bijou91-picoctf@webshell:~$ unzip challenge.zip
Archive:  challenge.zip
   creating: drop-in/
   creating: drop-in/.git/
   creating: drop-in/.git/branches/
  inflating: drop-in/.git/description  
   creating: drop-in/.git/hooks/
  inflating: drop-in/.git/hooks/applypatch-msg.sample  
  inflating: drop-in/.git/hooks/commit-msg.sample  
  inflating: drop-in/.git/hooks/fsmonitor-watchman.sample  
  inflating: drop-in/.git/hooks/post-update.sample  
  inflating: drop-in/.git/hooks/pre-applypatch.sample  
  inflating: drop-in/.git/hooks/pre-commit.sample  
  inflating: drop-in/.git/hooks/pre-merge-commit.sample  
  inflating: drop-in/.git/hooks/pre-push.sample  
  inflating: drop-in/.git/hooks/pre-rebase.sample  
  inflating: drop-in/.git/hooks/pre-receive.sample  
  inflating: drop-in/.git/hooks/prepare-commit-msg.sample  
  inflating: drop-in/.git/hooks/update.sample  
   creating: drop-in/.git/info/
  inflating: drop-in/.git/info/exclude  
   creating: drop-in/.git/refs/
   creating: drop-in/.git/refs/heads/
 extracting: drop-in/.git/refs/heads/master  
   creating: drop-in/.git/refs/tags/
 extracting: drop-in/.git/HEAD       
  inflating: drop-in/.git/config     
   creating: drop-in/.git/objects/
   creating: drop-in/.git/objects/pack/
   creating: drop-in/.git/objects/info/
   creating: drop-in/.git/objects/0e/
 extracting: drop-in/.git/objects/0e/0fefcdc9c9722914a7a9ecab1e88784f005eeb  
   creating: drop-in/.git/objects/5b/
 extracting: drop-in/.git/objects/5b/222fb49097fe9874695e8cc7cd9a6c80886017  
   creating: drop-in/.git/objects/b5/
 extracting: drop-in/.git/objects/b5/62f0b425907789d11d2fe2793e67592dc6be93  
   creating: drop-in/.git/objects/d5/
 extracting: drop-in/.git/objects/d5/52d1ecd2d83fa2e65b6724d1ff73b45a7d59b7  
   creating: drop-in/.git/objects/0c/
 extracting: drop-in/.git/objects/0c/1ab266b7a3a1cd099bb509f82b7a2d03aecd03  
   creating: drop-in/.git/objects/42/
 extracting: drop-in/.git/objects/42/942c9c605b30100f5d859ef6e172027447c0db  
  inflating: drop-in/.git/index      
 extracting: drop-in/.git/COMMIT_EDITMSG  
   creating: drop-in/.git/logs/
  inflating: drop-in/.git/logs/HEAD  
   creating: drop-in/.git/logs/refs/
   creating: drop-in/.git/logs/refs/heads/
  inflating: drop-in/.git/logs/refs/heads/master  
 extracting: drop-in/message.txt     
Bijou91-picoctf@webshell:~$ ls
README.txt  challenge.zip  drop-in
Bijou91-picoctf@webshell:~$ cd drop-in
Bijou91-picoctf@webshell:~/drop-in$ ls -la
total 4
drwxr-xr-x 3 Bijou91-picoctf Bijou91-picoctf  49 Mar 12  2024 .
drwxr-xr-x 3 Bijou91-picoctf Bijou91-picoctf 191 Feb 17 04:15 ..
drwxr-xr-x 8 Bijou91-picoctf Bijou91-picoctf 166 Mar 12  2024 .git
-rw-r--r-- 1 Bijou91-picoctf Bijou91-picoctf  11 Mar 12  2024 message.txt
Bijou91-picoctf@webshell:~/drop-in$ cat message.txt
TOP SECRET
Bijou91-picoctf@webshell:~/drop-in$ git reflog
Bijou91-picoctf@webshell:~/drop-in$ git checkout b562f0b
Note: switching to 'b562f0b'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at b562f0b create flag
Bijou91-picoctf@webshell:~/drop-in$ ls
message.txt
Bijou91-picoctf@webshell:~/drop-in$ cat message.txt
picoCTF{s@n1t1z3_c785c319}
```

picoCTF{s@n1t1z3_c785c319}
## Notas
