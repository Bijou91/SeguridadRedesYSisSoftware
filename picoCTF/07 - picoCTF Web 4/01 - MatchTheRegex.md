# MatchTheRegex

## Descripción
How about trying to match a regular expression
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan es este campo para ingresar nuestro input
![[01MatchRegex01.png]]

Si intentamos ingresar algo, nos da este error 
![[01MatchRegex02.png]]

Al analizar el código fuente de la página, encontramos este script de JavaScript, donde resalta la línea de comentario con lo que parece una pista
```
<script>
	function send_request() {
		let val = document.getElementById("name").value;
		// ^p.....F!?
		fetch(`/flag?input=${val}`)
			.then(res => res.text())
			.then(res => {
				const res_json = JSON.parse(res);
				alert(res_json.flag)
				return false;
			})
		return false;
	}
</script>
```

Usamos regexr y le pasamos el comentario de la pista, y este nos indica que entre p y F, van 5 caracteres excluyendo saltos de línea, así que rellenamos con números de 1 - 5 
![[01MatchRegex03.png]]

Probamos con esto en la página, y nos entrega la flag
![[01MatchRegex04.png]]

picoCTF{succ3ssfully_matchtheregex_08c310c6}
## Notas
