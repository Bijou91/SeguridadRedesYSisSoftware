# Insp3ct0r

## Descripción
Kishor Balan tipped us off that the following code may need inspection
## Solución
### Solución:
Al abrir la página web, y seleccionar la sección 'How', obtenemos esta información
![[01inspector01.png]]
Como vemos, se nos mencionan 3 herramientas usadas para la web, que es donde buscaremos la flag.

Empezamos con HTML, inspeccionando la página
![[01inspector02.png]]
Obtenemos la primera parte de la flag:
picoCTF{tru3_de

Seguimos con la hoja de estilos
![[01inspector03.png]]
Otra parte de la flag:
t3ct1ve_0r_ju5t

Y por último, el script de JavaScript
![[01inspector04.png]]
La última parte de la flag
_ lucky?302945a7}

#### Flag completa
picoCTF{tru3_det3ct1ve_0r_ju5t_lucky?302945a7}
## Notas
