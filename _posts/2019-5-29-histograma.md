---
layout: post
comments: true
mathjax: true
title: 2.4| Histograma 
---

El _Histograma_ es una buena caracterización inicial de una imagen, nos permite observar de manera sencilla la distribución de las intensidades que tiene una imagen en particular, y con esto, diseñar una estrategia para mejorarla.

Se encuentra definido como una función unidimensional discreta, de la forma:

{: .center}
$$H[r] = n$$

En donde la variable independiente $$r$$ corresponde a los niveles de brillo de la imagen (en el histograma se les nombra usualmente como bins). Por otro lado, la variable dependiente $$n$$ indica el número de pixeles que cuentan con esa intensidad. Consideremos el caso que se observa en la __Figura 2.1__, en la cual contamos con una imagen de tamaño 5 x 5 (25 pixeles), con dos niveles de intensidad (0 para las casillas oscuras, 1 para las oscuras). El histograma de esta imagen en particular se muestra a la derecha, cuya altura de cada columna indica la cantidad de pixeles con ese nivel de intensidad.

{: .center}
![5x5]({{ site.baseurl }}/images/histograma5x5.PNG)
__Figura 2.1__ _A la izquierda se muestra una imagen de 5x5, en donde 5 pixeles corresponden al color oscuro y 20 al blanco. A la derecha se muestra su histograma, con el cual podemos observar rápidamente la cantidad de pixeles correspondientes a cada intensidad._
