# b00tl3gRSA2

## Descripción
In RSA d is a lot bigger than e, why don't we use d to encrypt instead of e?
Connect with nc fickle-tempest.picoctf.net 65323.
## Solución
Este reto nos presenta un escenario de RSA donde el exponente público e es extremadamente grande, casi del mismo orden de magnitud que n. Los valores obtenidos al conectarnos vía nc son:
```
c: 5935671994090548700... (valor de c)
n: 9268468934232288586... (valor de n)
e: 5799351596595258526... (valor de e)
```

Cuando e es muy grande, el exponente privado d suele ser muy pequeño, lo que hace que el sistema sea vulnerable al Ataque de Wiener.

Este es el código que usaremos:
```python
import subprocess
import re
import os

# Configuración de los datos del reto
# Sustituye estos valores con los que te dio el comando 'nc'
c = 59356719940905487007743043739702012991010705420375170840273360893257168427760868389742355166401523110203089526003646051919483329136972959900916184728794195803708543318389759518132992480653561678418825298606234964704672400194611625266964491947065305479913674292580764577737753256754752679955271519202823978852
n = 92684689342322885866374099742525000798357580802336978857747798910457008114195458841599620910697847734065761110348481224814127332312577340953569368308274208293796738951126587616572338084799067528116340177253408702340000052544680693303178025229834673402584030738436469379621157554816621920227524191016051185199
e = 57993515965952585268205787694611024424954595357758708699202953902697873441549249747737547563742414850097420782947955652317819239759858690823245175797143593166082330504514223472905727606976413451238766782086142740292145656938008728451067579845099821472568670889961492652232417637120648124745127715175664977569

# Ruta al script de RsaCtfTool
# Usamos la ruta relativa basada en tu estructura actual
script_path = "src/RsaCtfTool/main.py"

# Comando para ejecutar Wiener Attack específicamente para no saturar el CPU
command = [
    "python3", script_path,
    "-n", str(n),
    "-e", str(e),
    "--decrypt", str(c),
    "--attack", "wiener"
]

print("[*] Lanzando RsaCtfTool (Wiener Attack)...")

# Ejecución con PYTHONPATH configurado internamente
env = os.environ.copy()
env["PYTHONPATH"] = env.get("PYTHONPATH", "") + ":" + os.path.join(os.getcwd(), "src")

try:
    result = subprocess.run(command, capture_output=True, text=True, env=env)
    
    # Buscamos la flag en el output usando regex
    flag = re.search(r'picoCTF\{.*\}', result.stdout)
    
    if flag:
        print("\n[+] Flag encontrada:")
        print(flag.group(0))
    else:
        print("\n[-] No se encontró la flag en el output.")
        print("DEBUG OUTPUT:\n", result.stdout)
        if result.stderr:
            print("DEBUG ERRORS:\n", result.stderr)

except Exception as error:
    print(f"[!] Error al ejecutar el script: {error}")
```

Y esta es la salida que obtenemos, junto a nuestra bandera.
```
┌──(venv)─(kali㉿kali)-[~/RsaCtfTool]
└─$ python3 solve_rsa.py
[*] Lanzando RsaCtfTool (Wiener Attack)...

[-] No se encontró la flag en el output.
DEBUG OUTPUT:
 
DEBUG ERRORS:
 private argument is not set, the private key will not be displayed, even if recovered.

[*] Testing key /tmp/tmp9vcn3h6_.
[*] Performing wiener attack on /tmp/tmp9vcn3h6_.

  0%|          | 0/338 [00:00<?, ?it/s]
  4%|▎         | 12/338 [00:00<00:00, 101067.57it/s]
[+] Time elapsed: 0.0482 sec.
[+] Total time elapsed min,max,avg: 0.0482/0.0482/0.0482 sec.

Results for /tmp/tmp9vcn3h6_:

Decrypted data :
HEX : 0x7069636f4354467b6261645f31643361355f333830313235357d
INT (big endian) : 180638594769037903267909311328535969949661653394344568289572221
INT (little endian) : 201201246288020047469268860767203668385040408164319000355105136
utf-8 : picoCTF{bad_1d3a5_3801255}
utf-16 : 楰潣呃筆慢彤搱愳張㠳㄰㔲紵
STR : b'picoCTF{bad_1d3a5_3801255}'
HEX : 0x0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000007069636f4354467b6261645f31643361355f333830313235357d
INT (big endian) : 180638594769037903267909311328535969949661653394344568289572221
INT (little endian) : 87923937388916367800868352403628292040472005935986907473300303883800619548571958192653049876691246183686213055914703595788903787435491398309281599513738061257805505300877968446411349796977165839200212532432248072420708003309027116616432248075642769163888226929019343468731992795354133832953251357773210320896
utf-8 : picoCTF{bad_1d3a5_3801255}
utf-16 : 楰潣呃筆慢彤搱愳張㠳㄰㔲紵
STR : b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00picoCTF{bad_1d3a5_3801255}'
```

picoCTF{bad_1d3a5_3801255}
## Notas
- 