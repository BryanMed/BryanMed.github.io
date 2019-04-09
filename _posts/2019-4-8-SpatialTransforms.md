---
layout: post
comments: true
mathjax: true
title: 2. Transformaciones en el dominio espacial
---
## 2.1 Funciones de transformación de intensidad

Este conjunto de métodos _manipula directamente_ los pixeles de la imagen, en donde estas operaciones están expresadas de la forma:

$$ g(x, y) = T[f(x, y)] $$

en donde las transformaciones _T_, son básicamente funciones encargadas de _mapear_ las intensidades de los pixeles de entrada _f(x, y)_, a las de una imagen de salida _g(x, y)_.

Tomemos como ejemplo la función de transformacion mostrada en la __Figura 2.1__. En donde se observa que por cada nivel de intensidad de la imagen de entrada, le corresponde el mismo valor en la imagen de salida, por lo tanto, el efecto que tiene esta transformación es nulo.


$$ r = h = \sqrt{\frac {1} {2}} = \sqrt{\frac {N} {N+1}} \sqrt{\frac {N+1} {2N}} $$
