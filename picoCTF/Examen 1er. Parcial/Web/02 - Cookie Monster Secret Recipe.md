## Cookie Monster Secret Recipe
# Descripción
Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe?
You can access the Cookie Monster [here](http://verbal-sleep.picoctf.net:60213/) and good luck
# Solución
Al entrar a la página nos topamos con este login
![inicioCMSR](https://blog.qz.sg/content/images/2025/03/cookie_monster_secret_recipe-site.webp)

Comenzaremos con test:test como credenciales para validarnos, pero no hay ningún tipo de login.

Ahora, como nos indica en la pista del sitio web, checaremos las cookies dentro de las herramientas de desarrollador, donde encontramos una cookie con nombre 'secret_recipe' y un valor que parece estar encriptado
![cookieMonsterSR](https://blog.qz.sg/content/images/2025/03/cookie_monster_secret_recipe-cookie.webp)

Así que ahora usaremos CyberChef para desencriptar desde base64 para obtener nuestra bandera.

picoCTF{c00k1e_m0nster_l0ves_c00kies_C430AE20}
# Notas adicionales
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=Y0dsamIwTlVSbnRqTURCck1XVmZiVEJ1YzNSbGNsOXNNSFpsYzE5ak1EQnJhV1Z6WDBNME16QkJSVEl3ZlElM0QlM0Q&oeol=CR
# Referencias
- Imágenes tomadas de aquí: https://blog.qz.sg/picoctf-2025-web-exploitation-writeups/