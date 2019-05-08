---
layout: post
comments: true
mathjax: true
title: 2.1| Imagen negativa/complemento (Intro a transformaciones espaciales)
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
![negativeImage]({{ site.baseurl }}/images/negativeImage.PNG)
 __Figura 2.3__ _En este caso, la imagen de entrada es el complemento a la imagen de salida, si sumamos ambas imágenes obtendriamos una imagen totalmente blanca_.
 
 De igual manera, en la __Figura 2.4__ se muestra de manera mas detallada este proceso, por ejemplo, a un pixel en la imagen de entrada $$f(i, j) = 200$$ le corresponderá $$g(i, j) = 55$$, en la gráfica del medio se muestra la recta que mapea a estas intensidades. 
 
 {: .center}
![negativeImageVS]({{ site.baseurl }}/images/negativeImageVS.PNG)
 __Figura 2.4__ _Con esta transformación, a cada pixel de entrada le corresponde el complemento en el pixel de salida_.
 
 Esta transformación tiene múltiples aplicaciones, en donde objetos claros rodeados de un fondo oscuro no son del todo bien percibidos por el ojo humano, en cambio, objetos claros en fondo oscuro si que si, por ejemplo, en la __Figura 2.5__ se muestran unas lesiones adquiridas por tuberculosis, en donde en la imagen de la derecha se le aplica la transformación negativa en favor de una mejor visualización de estas regiones.
 
 {: .center}
![chest]({{ site.baseurl }}/images/chest.PNG)
 __Figura 2.5__ _A la izquierda encontramos una imagen adquirida por rayos X, en donde un paciente cuenta con lesiones producidas por tuberculosis (complejo de Ghon), a la derecha se aplicó la transformación negativa de esta imagen para ayudar a una mejor comprensión de los detalles.  (imagen tomada de [aqui](https://en.wikipedia.org/wiki/Tuberculosis_radiology#/media/File:Chest_x-ray_of_Ghon%27s_complex_of_active_tuberculosis.jpg)) _.
 
 ## Referencias
 [capitulo 3 del libro de Gonzalez](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)
 
 
 
