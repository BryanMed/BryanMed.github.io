---
layout: post
comments: true
mathjax: true
title: 3.3| Convolución - tipos de kernels y sus aplicaciones.
--- 

En el post anterior hablamos acerca del cómo se realiza el proceso de [convolución](https://bryanmed.github.io/conv2d/), esta vez veremos la importancia de los _kernels (filtros, máscaras, ventanas)_ y algunas de sus aplicaciones en el procesamiento digital de imágenes.

### Operador identidad

El operador identidad dentro del proceso de convolución, es aquél que devuelve el mismo valor que la entrada ($$g[x, y] = f[x, y]$$). Regresemos un poquito a las señales. El operador identidad está definido como:

$$w = [0 \quad 1 \quad 0 ]$$

En el ejemplo de la __Figura 1__ encontramos una señal de electrocardiograma, la cual haremos convolucionar con la señal anterior $$w$$, y como podemos observar, es la misma señal resultante.

{: .center} 
![ecgIdentidad]({{ site.baseurl }}/images/zorroOscuro.PNG)
__Figura 1__ _Al utilizar el operador identidad obtenemos exactamente la misma señal a la salida_.

Ahora pasemos a imágenes, en este caso el operador identidad está definido por la matriz (en este caso de 3x3 pero puede ser de cualquier tamaño impar):

$$
w = \begin{vmatrix}
0&0&0\\
0&1&0\\
0&0&0\\
\end{vmatrix}
$$

Y en la __Figura 2__ podemos observar el resultado, el cual es la misma imagen que la entrada.

{: .center} 
![ecgIdentidad]({{ site.baseurl }}/images/zorroOscuro.PNG)
__Figura 2__ _Al utilizar el operador identidad obtenemos exactamente la misma imagen a la salida_.


### Operador para modificar la amplitud
En este caso, al multiplicar el operador identidad con algún valor deseado, podemos modificar la amplitud de la señal. Por ejemplo, veamos las siguientes máscaras:

$$w_2 = [0 \quad 2 \quad 0 ] \qquad \qquad \qquad w_{0.5} = [0 \quad 0.5 \quad 0 ]$$

Al ver su composición podemos intuir que la señal $$w_2$$ duplicará la amplitud de la señal, y caso contrario con la señal $$w_{0.5}$$, y esto lo podemos ver en la __Figura 3__ en donde se hizo convolucionar la señal de ECG con las señales anteriores.

{: .center} 
![ecg205]({{ site.baseurl }}/images/zorroOscuro.PNG)
__Figura 3__ _En la izquierda podemos observar el resultado de convolucionar el ECG con el kernel $$w_2$$, en la derecha al hacerlo con $$w_{0.5}_.

Ahora en el caso de las imágenes, las matrices correspondiente a ambos casos anteriores se encuentran de la forma:

$$
w_2 = \begin{vmatrix}
0&0&0\\
0&2&0\\
0&0&0\\
\end{vmatrix}

\qquad \qquad \qquad

w_{0.5} = \begin{vmatrix}
0&0&0\\
0&0.5&0\\
0&0&0\\
\end{vmatrix}
$$

En donde el efecto de realizar la convolución de la imagen de entrada con el kernel $$w_2$$ será el de generar una imagen más clara, debido a que estamos _duplicando_ la _amplitud_ de los niveles de gris. Caso contrario con el kernel $$w_{0.5}$$ en donde _partimos a la mitad_ estas intensidades, por lo cual la imagen se vuelve un tanto oscura, como se muestra en la __Figura 4__.

{: .center} 
![imgDark&light]({{ site.baseurl }}/images/zorroOscuro.PNG)
__Figura 4__ _En la izquierda podemos observar el resultado de convolucionar la imagen con el kernel $$w_2$$, en la derecha al hacerlo con $$w_{0.5}_.

### Operador de desplazamiento

Ahora consideremos que el valor de la señal no se encuentra centrado, por ejemplo el kernel $$w_{desp20}$$ muestra una señal en donde el origen se encuentra desplazado 20 unidades, como se muestra a continuación.

$$w_{desp20} = [\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 1]$$







