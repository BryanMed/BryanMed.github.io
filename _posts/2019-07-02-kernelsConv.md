---
layout: post
comments: true
mathjax: true
title: 3.3| Convolución - tipos de kernels y sus aplicaciones.
--- 

En el post anterior hablamos acerca del cómo se realiza el proceso de [convolución](https://bryanmed.github.io/conv2d/), esta vez veremos la importancia de los _kernels (filtros, máscaras, ventanas)_ y algunas de sus aplicaciones en el procesamiento digital de imágenes.

### Operador identidad

El operador identidad dentro del proceso de convolución, es aquél que devuelve el mismo valor que la entrada ($$g[x, y] = f[x, y]$$). Regresemos un poquito a las señales. El operador identidad está definido como:

$$w = [0 \; 1 \; 0 ]$$

En el ejemplo de la __Figura 1__ encontramos una señal de electrocardiograma, la cual haremos convolucionar con la señal anterior $$w$$, y como podemos observar, es la misma señal resultante.

{: .center} 
![ecgIdentidad]({{ site.baseurl }}/images/zorroOscuro.PNG)
__Figura 1__ _Al utilizar el operador identidad obtenemos exactamente la misma señal a la salida_.

Ahora pasemos a imágenes, en este caso el operador identidad está definido por la matriz (en este caso de 3x3 pero puede ser de cualquier tamaño impar):

$$
\begin{vmatrix}
0&0&0\\
0&1$0\\
0&0&0\\
\end{vmatrix}
$$






