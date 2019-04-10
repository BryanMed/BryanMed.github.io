---
layout: post
comments: true
mathjax: true
title: 2. Transformaciones en el dominio espacial
---
## 2.1 Funciones de transformación de intensidad

Este conjunto de métodos _manipula directamente_ los pixeles de la imagen, en donde estas operaciones están expresadas de la forma:

$$ g(x, y) = T[f(x, y)] $$

La transformación $$T$$ es básicamente una función encargada de __mapear__ las intensidades de los pixeles de entrada $$f(x, y)$$ a las de la imagen de salida $$g(x, y)$$.

Tomemos el caso mostrado en la __Gráfica 2.1__ en donde se observa la correspondencia que existe entre los niveles de intensidad de la imagen de entrada $$f(x, y)$$ es la misma respecto a aquellas en la imagen de salida $$g(x, y)$$, por lo tanto, la transformada $$T$$ en este ejemplo, es nula, esto se observa en la __Figura 2.1__ en donde no existe diferencia alguna entre ambas imagenes dado que tienen los mismos niveles de brillo en cada pixel.

{: .center}
![grafica1]({{ site.baseurl }}/images/grafica1a1.png)
{: .center}  
__Gráfica 2.1__ los niveles de brillo de la imagen de entrada son los mismos que los de la imagen de salida.

{: .center} 
![comparison1]({{ site.baseurl }}/images/transformada1.PNG)
{: .center}  
__Figura 2.1__ El efecto de la transformada $$T$$ es nulo, dado que $$g(x, y) = f(x, y)$$
