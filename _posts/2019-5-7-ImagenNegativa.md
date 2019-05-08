---
layout: post
comments: true
mathjax: true
title: 2.1| Imagen negativa/complemento
---
# (Intro a transformaciones espaciales)
## Funciones de transformación de intensidad en el dominio espacial

Cuando hablamos de los métodos que trabajan en el _dominio espacial_, nos referimos a las técnicas que manipulan _directamente_ los pixeles contenidos dentro del plano de la imagen. Estos procedimientos están denotados de la forma:

{: .center}
$$g(x, y) = T[f(x, y)]$$

Esta operación define básicamente una función $$T$$ que se encargará de _mapear_ las intensidades de los pixeles de la imagen de entrada $$f(x, y)$$, a otro valores en la imagen de salida $$g(x, y)$$. En el caso mostrado en la __Figura 2.1__ en el cual no se ha aplicado ninguna transformación a la imagen de entrada, lógicamente se obtiene una imagen de salida idéntica a la inicial.

{: .center}
![sameImage]({{ site.baseurl }}/images/sameImage.PNG)
 __Figura 2.1__ _Al no aplicar ninguna transformación, obtenemos la misma imagen_.

Como podemos notar, ambas imágenes son iguales, es decir, que el brillo de los pixeles de salida está definido por $$g(x,y) = f(x, y)$$. Digamos que tomamos un pixel aleatorio de la imagen de entrada, cuya posición son las coordenadas $$(i, j)$$ y el cual tiene un brillo de 200 (trabajamos con imágenes Uint8 cuyo rango de intensidad va de 0 a 255), en pocas palabras $$f(i, j) = 200$$, con lo cual, siguiendo las cantinfleada que me aventé, podemos intuir que el pixel en la salida con la misma posición tendrá el brillo correspondiente ($$g(x, y) = 200$$, esto queda ejemplificado en la __Figura 2.2__

{: .center}
![sameImageVS]({{ site.baseurl }}/images/sameImageVS.PNG)
 __Figura 2.2__ _Aquí, las intensidades en la imagen de salida corresponden con aquellas en la imagen de entrada_.
