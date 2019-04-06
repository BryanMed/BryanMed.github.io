---
layout: post
mathjax: true
title: Procesamiento Digital de Imágenes - Introducción
---


## 1.1 ¿Qué es una imagen digital?

Una __imagen digital__ es una función bidimensional _f(x, y)_, en donde _f_ se refiere al nivel de intensidad (brillo) 
que se encuentra en determinada posición (x, y). Los sistemas de adquisición de estas imágenes, consisten en un arreglo de sensores, 
encargados de medir la intensidad de la luz que llega a cada uno de estos. Este proceso de __muestreo__ tiene como resultado, 
que tanto las coordenadas, así como los niveles de brillo, sean de naturaleza discreta. La _Figura 1.1_ ejemplifica una imagen 
continua respecto a una imagen digital.

![Parroquia]({{ site.baseurl }}/images/iglesia.png)
> _Figura 1.1_ Parroquia de Nuestra Señora de la Asunción, Lagos de Moreno, Jal. La imagen de la izquierda es una representación de una imagen continua, y a la derecha se simula una imagen digital (adquirida por mi poderosísimo Alcatel), donde se observa la constitución discreta de la imagen. 

$$
\begin{align}
P(Y \mid do(X)) &= \sum_U P(Y \mid X, U=u) P(U=u) \tag{iff all back doors are shut} \\
&= \mathbb E_{u\sim U}[P(Y \mid X, U=u)] \\
P(Y \mid X, U=u) &=  \frac{\mathbb E_{(x, y)\sim X, Y, U=u} [(x -\mu_x)(y-\mu_y)]}{\sigma_x} \tag{correlation}  \\
\\
Y &= aX + bU + c \tag{assume linear relationships} \\
a&= (Y-bU + c)X^{-1} \\
\end{align}
$$

jala parillo
