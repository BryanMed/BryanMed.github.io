---
layout: post
comments: true
mathjax: true
title: 2.1| Imagen negativa/complemento _(Intro a transformaciones espaciales)_
---
## Funciones de transformación de intensidad en el dominio espacial

Cuando hablamos de los métodos que trabajan en el _dominio espacial_, nos referimos a las técnicas que manipulan _directamente_ los pixeles contenidos dentro del plano de la imagen. Estos procedimientos están denotados de la forma:

{: .center}
$$g(x, y) = T[f(x, y)]$$

Esta expresión básicamente define una función $$T$$ que se encargará de _mapear_ las intensidades de los pixeles de la imagen de entrada $$f(x, y)$$, a otro valores en la imagen de salida $$g(x, y)$$. Por ejemplo, en el caso mostrado en la __Figura 2.1__ no se aplica ninguna transformación a la imagen de entrada, por lo que lógicamente la imagen de salida es prácticamente una copia.

{: .center}
![sameImage]({{ site.baseurl }}/images/sameImage.PNG)
 __Figura 2.1__ _Al no aplicar ninguna transformación, obtenemos la misma imagen_.

Como podemos notar, ambas imágenes son iguales, es decir, que el brillo de los pixeles de salida queda definido por la expresión $$g(x,y) = f(x, y)$$, bien, tomemos como referencia un pixel cualquiera de la imagen de entrada, cuya posición está determinada por las coordenadas $$(i, j)$$ y el cual tiene un brillo de 200 (trabajamos con imágenes Uint8 cuyo rango de intensidad va de 0 a 255), en pocas palabras $$f(i, j) = 200$$. Por lo tanto, la intensidad del pixel en esas mismas coordenadas será la misma ($$g(x, y) = 200$$). Esto se muestra en la __Figura 2.2__.

{: .center}
![sameImageVS]({{ site.baseurl }}/images/sameImageVS.PNG)
 __Figura 2.2__ _Aquí, las intensidades en la imagen de salida corresponden con aquellas en la imagen de entrada_.


## Imagen Negativa/Complemento

Ahora proseguiremos con una de las transformadas más sencillas, en donde obtendremos el _negativo_ de la imagen de entrada, en donde se espera que la intensidad de los pixeles en la imagen de salida sea _complementaria_ a aquella de la imagen de entrada. Para lograrlo, consideramos que la suma de ambas intensidades, debe ser igual $$L-1$$ el cual es la cantidad de niveles de brillo de una imagen (Recuerdas el formato Uint8, pues en ese caso serían 255), de la forma:

{: .center}
$$f(x, y) + g(x, y) = L-1$$

Así, para obtener la imagen de salida, hacemos un despejillo para obtener $$g(x, y)$$:

{: .center}
$$g(x, y) = (L-1) - f(x, y)$$

Y ahora si ya estamos ready to go, en la __Figura 2.3__ observamos el efecto de esta transformación.

{: .center}
![sameImageVS]({{ site.baseurl }}/images/sameImageVS.PNG)
 __Figura 2.2__ _Aquí, las intensidades en la imagen de salida corresponden con aquellas en la imagen de entrada_.
