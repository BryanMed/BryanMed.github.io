---
layout: post
comments: true
title: 2. Transformaciones en el dominio espacial
---

Son un conjunto de métodos caracterizados por _manipular_ directamente los pixeles de la imagen. Estas técnicas se encuentran de la forma

![spatialtrans]({{ site.baseurl }}/images/spatialTrans.png)

en donde las transformaciones _T_, son básicamente funciones encargadas de _mapear_ las intensidades de los pixeles de entrada _f(x, y)_, a las de una imagen de salida _g(x, y)_.

Tomemos como ejemplo la función de transformacion mostrada en la __Figura 2.1__. En donde se observa que por cada nivel de intensidad de la imagen de entrada, le corresponde el mismo valor en la imagen de salida, por lo tanto, el efecto que tiene esta transformación es nulo.
