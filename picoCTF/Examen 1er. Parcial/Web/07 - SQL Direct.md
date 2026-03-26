## SQL Direct
# Descripción
Connect to this PostgreSQL server and find the flag!
`psql -h saturn.picoctf.net -p 55399 -U postgres pico`
Password is `postgres`
# Solución
Lo primero que haremos es conectarnos al postgreSQL
```
└─$ psql -h saturn.picoctf.net -p 55399 -U postgres pico
Password for user postgres: 
psql (18.1 (Debian 18.1-1), server 15.2 (Debian 15.2-1.pgdg110+1))
Type "help" for help.

pico=#
```

Ahora, usaremos un `\dt` para ver las tablas del esquema público
```
pico=# \dt
          List of tables
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | flags | table | postgres
(1 row)
```

Ahora usaremos el comando `select`, tomando la tabla 'flags' del esquema público
```
pico=# select * from public.flags;
 id | firstname | lastname  |                address                 
----+-----------+-----------+----------------------------------------
  1 | Luke      | Skywalker | picoCTF{L3arN_S0m3_5qL_t0d4Y_31fd14c0}
  2 | Leia      | Organa    | Alderaan
  3 | Han       | Solo      | Corellia
(3 rows)
```

picoCTF{L3arN_S0m3_5qL_t0d4Y_31fd14c0}
# Notas adicionales
- 
# Referencias
- 