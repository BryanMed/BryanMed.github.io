---
layout: post
comments: true
mathjax: true
title: 1. Procesamiento Digital de Imágenes
---
## ¿Qué es una imagen digital?

Una __imagen digital__ es una función bidimensional _f(x, y)_, en donde _f_ se refiere al nivel de intensidad (brillo) 
que se encuentra en determinada posición (x, y). Los sistemas de adquisición de estas imágenes, consisten en un arreglo de sensores, 
encargados de medir la intensidad de la luz que llega a cada uno de estos. Este proceso de __muestreo__ tiene como resultado, 
que tanto las coordenadas, así como los niveles de brillo, sean de naturaleza discreta. La __Figura 1.1__ ejemplifica una imagen 
continua respecto a una imagen digital.

{: .center}
![Parroquia]({{ site.baseurl }}/images/iglesia.png)
__Figura 1.1__ _Parroquia de Nuestra Señora de la Asunción, Lagos de Moreno, Jal. La imagen de la izquierda es una representación de una imagen continua, y a la derecha se simula una imagen digital (adquirida por mi poderosísimo Alcatel), donde se observa la constitución discreta de la imagen_. 

Estas imágenes son representadas como una matriz de $$M \times N)$$ elementos de la forma:

$$
f(x, y) = \begin{bmatrix}
f(0,0) & f(0,1) & ... & f(0, N-1)\\ 
f(1,0) & f(1,1) & ... & f(1, N-1)\\ 
... & ... &  & ... \\ 
f(M-1, 0) & f(M-1, 1) & ... & f(M-1, N-1)
\end{bmatrix}
$$

{: .center}
![grafica]({{ site.baseurl }}/images/CodeCogsEqn (1).png)

En donde cada elemento de este arreglo es conocido como __pixel__ (del inglés _picture element_), y es la unidad mínima
por la cual está conformada una imagen. En la __Figura 1.2__ se observa una imagen con niveles de intensidad binarios,
en donde, un valor de intensidad igual a 1 corresponde a un pixel color blanco, y negro en caso de ser 0. La formación del
corazón se da por la manera en la que están dispuesto el brillo de los pixeles en toda la imagen.

{: .center}
![corazón]({{ site.baseurl }}/images/corazonpixel.PNG) 
{: .center}
__Figura 1.2__ _Los pixeles definen la información contenida en la imagen, al especificar el nivel de brillo en determinada posición._

## Procesamiento de imágenes
Son un conjunto de técnicas que tiene como finalidad obtener una representación más adecuada de la imagen, o la extracción de características relevantes encaminadas a obtener información mas profunda. La __Figura 1.3__ muestra estos dos enfoques.

{: .center}
![corazón]({{ site.baseurl }}/images/imageprocessing.PNG)
 __Figura 1.3__ _La mejora de la imagen (image enhancement) y la extracción de características (feature extraction) son los dos principales objetivos que plantea el procesamiento de imágenes._

### Bibliografía utilizada
