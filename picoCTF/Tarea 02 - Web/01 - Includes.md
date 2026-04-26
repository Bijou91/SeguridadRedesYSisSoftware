# Includes

## Descripción
Can you get the flag?
## Solución
### Solución:
Al entrar a la página, obtenemos esta pantalla, incluyendo el botón 'Say hello'
![[01Includes01.png]]

Al pulsar el 'say hello', obtenemos este código de error
![[01Includes02.png]]

Entonces, lo que haremos ahora es inspeccionar el código fuente de la página, donde encontramos la hoja de estilos y el script de JavaScript
![[01Includes03.png]]

Al buscar en la hoja de estilos, encontramos una parte de la flag:
```css
body {
  background-color: lightblue;
}

/*  picoCTF{1nclu51v17y_1of2_  */
```

Mientras que en el archivo de JavaScript, está la otra parte
```javascript
function greetings()
{
  alert("This code is in a separate file!");
}

//  f7w_2of2_df589022}
```

picoCTF{1nclu51v17y_1of2_f7w_2of2_df589022}
## Notas
