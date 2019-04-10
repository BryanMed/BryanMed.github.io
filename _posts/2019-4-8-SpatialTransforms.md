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

Tomemos el caso mostrado en la __Figura 2.1__ en donde la función de transformación $$T$$ tiene un efecto nulo, dado que los niveles de gris de la imagen de entrada es el mismo para la imagen de salida, es decir $$ g(x, y) = f(x, y) $$.
{: .center}![grafica1]({{ site.baseurl }}/images/grafica1a1.png)
{: .center}![comparison1]({{ site.baseurl }}/images/transformada1.PNG)

