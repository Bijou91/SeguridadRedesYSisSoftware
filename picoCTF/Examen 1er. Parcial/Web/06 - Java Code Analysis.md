## Java Code Analysis
# Descripción
BookShelf Pico, my premium online book-reading service.
I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book!
Here are the credentials to get you started:
- Username: "user"
- Password: "user"

Source code can be downloaded [here](https://artifacts.picoctf.net/c/479/bookshelf-pico.zip).
Website can be accessed [here!](http://saturn.picoctf.net:52521/).
# Solución
Al entrar a la página que nos entregan, nos topamos con este login
![[06Java01.png]]

Al entrar a la página, notamos que hay varios libros, uno llama la atención, uno llamado 'FLAG'
![libro](https://miro.medium.com/v2/resize:fit:720/format:webp/1*-JOdHvxuGnqeniIvTFBzUw.png)

Si usamos BURP para interceptar el paquete al momento de intentar seleccionar este libro 'FLAG'
![package](https://cseciitb.github.io/_astro/JCAburp.CutlSXkN_Z28QMH9.webp)

Al decodificar esta cadena de texto con [jwt.io](jwt.io), vemos la información que contiene
![info](https://cseciitb.github.io/_astro/JCAjwt.DttiUQT4_1gTmgl.webp)

Ahora que sabemos esta información, debemos encontrar la llave secreta que nos deje encriptar la información que usaremos para saltarnos la verificación

Esto lo encontraremos en el código fuente, precisamente en el archivo `SecretGenerator.java`. El cual nos entrega la llave de encriptación.
```java
private String generateRandomString(int len) {
        // not so random
        return "1234";
    }
```

Para encontrar el userID que buscamos
```
private Integer value; 
//higher the value, more the privilege. By this logic, admin is supposed to have the highest value
```

Como no nos da un número exacto, solamente lo incrementaremos a 2, y modificaremos el rol y el email a Admin:admin para obtener un nuevo token
![nuevo token](https://brandon-t-elliott.github.io/screenshots/picoctf2023/jwt-decode.png)

Luego simplemente reemplazamos valores del token
![reemplazoToken](https://brandon-t-elliott.github.io/screenshots/picoctf2023/inspect.png)

Y obtenemos nuestra bandera
![[06Java02.png]]

picoCTF{w34k_jwt_n0t_g00d_d7c2e335}
# Notas adicionales
Imágenes tomadas de:
- https://cseciitb.github.io/posts/PicoCTFJavaCodeAnalysis/
- https://brandon-t-elliott.github.io/java-code-analysis
# Referencias
- 