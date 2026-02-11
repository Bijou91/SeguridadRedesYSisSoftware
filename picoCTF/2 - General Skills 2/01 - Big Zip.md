# Big Zip

## Descripción
Unzip this archive and find the flag.
## Solución
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/01-BigZip]
└─$ unzip big-zip-files.zip 
Archive:  big-zip-files.zip
   creating: big-zip-files/
 extracting: big-zip-files/jpvaawkrpno.txt  
  inflating: big-zip-files/oxbcyjsy.txt  
  inflating: big-zip-files/hllhxlvvdgiii.txt  
  inflating: big-zip-files/bdvnqbuutefealgveyiqd.txt  
  inflating: big-zip-files/fudfsewmaafsbniiyktzr.txt  
   creating: big-zip-files/folder_fqmjtuthge/
  inflating: big-zip-files/folder_fqmjtuthge/file_eaigogtrdslbxenbnfisxepj.txt  
  inflating: big-zip-files/folder_fqmjtuthge/file_ygocxgpzuxqjwfs.txt  
  inflating: big-zip-files/folder_fqmjtuthge/file_lqqprxhjtarithwygepdnlf.txt
....
....
....
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/01-BigZip]
└─$ grep -r "pico"
big-zip-files/folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:information on the record will last a billion years. Genes and brains and books encode picoCTF{gr3p_15_m4g1c_ef8790dc}

```

picoCTF{gr3p_15_m4g1c_ef8790dc}
## Notas
