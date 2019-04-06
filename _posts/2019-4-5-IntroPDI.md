---
layout: post
usemathjax: true
title: Procesamiento Digital de Imágenes
---
### ¿Qué es una imagen digital?

Una __imagen digital__ es una función bidimensional _f(x, y)_, en donde _f_ se refiere al nivel de intensidad (brillo) 
que se encuentra en determinada posición (x, y). Los sistemas de adquisición de estas imágenes, consisten en un arreglo de sensores, 
encargados de medir la intensidad de la luz que llega a cada uno de estos. Este proceso de __muestreo__ tiene como resultado, 
que tanto las coordenadas, así como los niveles de brillo, sean de naturaleza discreta. La _Figura 1.1_ ejemplifica una imagen 
continua respecto a una imagen digital.

![Parroquia]({{ site.baseurl }}/images/iglesia.png)
> _Figura 1.1_ Parroquia de Nuestra Señora de la Asunción, Lagos de Moreno, Jal. La imagen de la izquierda es una representación de una imagen continua, y a la derecha se simula una imagen digital (adquirida por mi poderosísimo Alcatel), donde se observa la constitución discreta de la imagen. 

Estas imágenes son representadas como una matriz de (M x N) elementos de la forma:
![grafica]({{ site.baseurl }}/images/CodeCogsEqn (1).png)

$$
\begin{bmatrix}
1 & 2\\ 
3 & 4
\end{bmatrix}
$$

Cada elemento de este arreglo es conocido como __pixel__ (del inglés _picture element_), y es la unidad mínima
por la cual está conformada una imagen. En la _Figura 1.2_ se observa una imagen con niveles de intensidad binarios,
en donde, un valor de intensidad igual a 1 corresponde a un pixel color blanco, y negro en caso de ser 0. La formación del
corazón se da por la manera en la que están dispuesto el brillo en los pixeles de toda la imagen.

![corazón]({{ site.baseurl }}/images/corazon.png)
> Figura 1.2 Los pixeles definen la información contenida en la imagen, al especificar el nivel de brillo en determinada posición.

### Procesamiento de imágenes
Son un conjunto de técnicas que tiene como finalidad obtener una representación más adecuada de la imagen, o la extracción de características relevantes encaminadas a obtener información mas profunda. La _Figurra 1.3_ muestra estos dos enfoques.



