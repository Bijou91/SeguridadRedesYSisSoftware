# Pixelated

## Descripción
I have these 2 images, can you make a flag out of them?
[scrambled1.png](https://challenge-files.picoctf.net/c_wily_courier/2180f74b7f56abc330252d0146f6a044f8e35027142e5cb16c9160c37a0c630f/scrambled1.png) [scrambled2.png](https://challenge-files.picoctf.net/c_wily_courier/2180f74b7f56abc330252d0146f6a044f8e35027142e5cb16c9160c37a0c630f/scrambled2.png)
## Solución
Para resolver este reto, lo que debemos hacer es combinar las 2 imágenes que nos entregan para que se elimine el ruido entre estas y que podamos leer la flag de forma clara.

Imagen 1:
![img1](https://challenge-files.picoctf.net/c_wily_courier/2180f74b7f56abc330252d0146f6a044f8e35027142e5cb16c9160c37a0c630f/scrambled1.png)

Imagen 2:
![img2](https://challenge-files.picoctf.net/c_wily_courier/2180f74b7f56abc330252d0146f6a044f8e35027142e5cb16c9160c37a0c630f/scrambled2.png)

Para poder mezclar estas dos imágenes, usaremos este código:
```python
import numpy as np
from PIL import Image

# Open images
im1 = Image.open("scrambled1.png")
im2 = Image.open("scrambled2.png")

# Make into Numpy arrays
im1np = np.array(im1)
im2np = np.array(im2)

# Add images
result = im2np + im1np
# Convert back to PIL image and save
Image.fromarray(result).save('result.png')
```

Y el resultado nos saldría así:
![imgresult](https://picoctf2021.haydenhousen.com/~gitbook/image?url=https%3A%2F%2F4273326122-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-MZKAlTji_ZhS27t6uHU%252Fuploads%252Fgit-blob-af517e3e6adda503163bb0dee51f668c63987580%252Fresult.png%3Falt%3Dmedia&width=300&dpr=1&quality=100&sign=1d579bc0&sv=2)

En mi caso, la bandera fue esta:
picoCTF{8cdf93c3}
## Notas
- Imagen de la imagen ya procesada viene de aquí: https://picoctf2021.haydenhousen.com/cryptography/pixelated