---
layout: post
comments: true
mathjax: true
title: PDI-3.3| Convolución - tipos de kernels y sus aplicaciones.
--- 

En el post anterior hablamos acerca del cómo se realiza el proceso de [convolución](https://bryanmed.github.io/conv2d/), esta vez veremos la importancia de los _kernels (filtros, máscaras, ventanas)_ y algunas de sus aplicaciones en el procesamiento digital de imágenes.

>Encontrarás la implementación de la convolución en [este](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/2.6%20Convolucion_correlacion) repositorio.


_______

{: .center} 
## Operador identidad

El operador identidad dentro del proceso de convolución, es aquél que devuelve el mismo valor que la entrada ($$g[x, y] = f[x, y]$$). Regresemos un poquito a las señales. El operador identidad está definido como:

$$w = [0 \quad \underline 1 \quad 0 ]$$

En donde la línea debajo del 1 indica que es el origen de la función (posición w[0]). En el ejemplo de la __Figura 1__ encontramos una señal de electrocardiograma, la cual haremos convolucionar con la señal anterior $$w$$, y como podemos observar, es la misma señal resultante.

{: .center} 
![ecgIdentidad]({{ site.baseurl }}/images/ecg1.PNG)
__Figura 1__ _Al utilizar el operador identidad obtenemos exactamente la misma señal en la salida (están superpuestas)_.

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
![ecgIdentidad]({{ site.baseurl }}/images/kernel1.PNG)
__Figura 2__ _Al utilizar el operador identidad obtenemos exactamente la misma imagen a la salida_.

_____

{: .center} 
## Operador para modificar la amplitud
En este caso, al multiplicar el operador identidad con algún valor deseado, podemos modificar la amplitud de la señal. Por ejemplo, veamos las siguientes máscaras:

$$w_2 = [0 \quad \underline 2 \quad 0 ] \qquad \qquad \qquad w_{0.5} = [0 \quad \underline 0.5 \quad 0 ]$$

Al ver su composición podemos intuir que la señal $$w_2$$ duplicará la amplitud de la señal, y caso contrario con la señal $$w_{0.5}$$, y esto lo podemos ver en la __Figura 3__ en donde se hizo convolucionar la señal de ECG con las señales anteriores.

{: .center} 
![ecg205]({{ site.baseurl }}/images/ecg2.PNG)
__Figura 3__ _En la izquierda podemos observar el resultado de convolucionar el ECG con el kernel $$w_2$$, en la derecha al hacerlo con $$w_{0.5}$$_.

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
![imgDark&light]({{ site.baseurl }}/images/kernel2.PNG)
__Figura 4__ _En la izquierda podemos observar el resultado de convolucionar la imagen con el kernel $$w_2$$, en la derecha al hacerlo con $$w_{0.5}$$_.

________

{: .center} 
## Operador de desplazamiento

Ahora consideremos que el valor de la señal no se encuentra centrado, por ejemplo el kernel $$w_{desp20}$$ muestra una señal en donde el origen se encuentra desplazado 20 unidades, como se muestra a continuación.

$$w_{desp20} = [\; \underline 0 \; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 0\; 1]$$

Lo que sucede con la señal al aplicar la convolución con esta función, es que la salida corresponderá al 20vo valor de la entrada. Algo así como $$g[x] =  f[x - 20]$$. Como se muestra en la __Figura 5__

{: .center} 
![ECGdesplazamiento]({{ site.baseurl }}/images/ecg3.PNG)
__Figura 5__ _Se observa como la señal de salida (en naranja) está desplazada 20 unidades respecto a la señal original (en azul)_.

¿Pasará algo similar con las imágenes? Pues si, aquí podemos controlar el desplazamiento de la imagen posicionando el 1 en cualquiera de los ejes alrededor del origen. Tomemos como ejemplo la matriz $$w_{desp2}$$:

$$
w_{desp2} = \begin{vmatrix}
0&0&0&0&0\\
0&0&0&0&0\\
0&0&0&0&1\\
0&0&0&0&0\\
0&0&0&0&0\\
\end{vmatrix}
$$

Que como podrás adivinar, la convolución de la imagen con este kernel resultará en un desplazamiento de la imagen en 2 unidades hacia la derecha, como se ejemplifica en la __Figura 6__.

{: .center} 
![ECGdesplazamiento]({{ site.baseurl }}/images/kernel3.PNG)
__Figura 6__ _El resultado de aplicar la convolución con el kernel $$w_desp2$$ es el desplazamiento de la imagen 2 pósiciones a la derecha_.

_________

{: .center} 
## Operadores de suavizado/promedio

El objetivo de este tipo de operadores es _suavizar_ las señales, esto es logrado al convolucionar la señal/imagen con una ventana que promediará el pixel de salida con su vecindad, también es conocido como _filtro pasa bajas_. Entre las ventajas encontramos que logra _reducir el ruido_, sin embargo, citando al tío Ben: "un gran poder conlleva una gran responsabilidad" y uno de los problemas es que también se da una _perdida de detalle_.

El operador de suavizado $$w_{suave}$$ en las señales tiene la siguiente forma:

$$w_{suave} = [\frac{1}{N} \qquad \cdots \qquad \underline{\frac{1}{N}} \qquad \cdots \qquad \frac{1}{N}]$$

En donde $$N$$ es el número de elementos del filtro. Como podemos ver, al realizar el proceso de convolución estaremos sustituyendo cada valor de la señal de entrada por la media que genera con los valores vecinos. Tomemos como ejemplo la siguiente máscara:

$$
w_{suave} = [\frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \underline{\frac{1}{15}} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15} \, \frac{1}{15}] 
$$

Al convolucionar con la señal de ECG, podemos observar en la parte izquierda de la __Figura 7__ como las diferencias en amplitud disminuyen, en la imagen derecha utilizamos una ventana con 101 elementos para evidenciar como las variaciones entre valores consecutivos son cada vez menores. 

{: .center} 
![ECGpromediado]({{ site.baseurl }}/images/ecg4.PNG)
__Figura 7__ _A la izquierda observamos el resultado de la señal al convolucionarlo con una ventana de promedio móvil de 15 elementos, a la derecha considerando 101_.

Como observamos, a medida que aumentamos el tamaño de este filtro, la señal se volverá más uniforme. Los kernels utilizados en imágenes para suavizar la imagen tienen una forma muy similar, como se muestra en la siguiente matriz $$w_{prom}$$.

$$
w_{prom} = \begin{vmatrix}
\frac{1}{N}&\cdots&\frac{1}{N}\\
\vdots&\frac{1}{N}&\vdots\\
\frac{1}{N}&\cdots&\frac{1}{N}\\
\end{vmatrix}
$$

En la __Figura 8__ aplicamos la convolución con una matriz de promediado de 3x3 $$w_{prom3x3}$$ y también con una matriz de tamaño 31x31.

$$
w_{prom3x3} = \begin{vmatrix}
\frac{1}{9}&\frac{1}{9}&\frac{1}{9}\\
\frac{1}{9}&\frac{1}{9}&\frac{1}{9}\\
\frac{1}{9}&\frac{1}{9}&\frac{1}{9}\\
\end{vmatrix}

\qquad

w_{prom31x31} = \begin{vmatrix}
\frac{1}{31}&\cdots&\frac{1}{31}\\
\vdots&\frac{1}{31}&\vdots\\
\frac{1}{31}&\cdots&\frac{1}{31}\\
\end{vmatrix}


$$

{: .center} 
![LenaSmooth]({{ site.baseurl }}/images/kernel4.PNG)
__Figura 8__ _A la izquierda observamos el resultado de la imagen al convolucionarla con una ventana de promedio móvil de 9 elementos, a la derecha considerando un filtro de 31x31_.

En la imagen anterior se evidencía la perdida de detalle que existe a medida que aumenta el tamaño del kernel de promediado, es decir, al igual que pasaba con la señal de ECG, las diferencias entre valores/pixeles vecinos van disminuyendo.

________

{: .center} 
## Operadores de Sharpening

El principal objetivo de los filtros de sharpening es el contrario al del operador de suavizado, aquí se espera _resaltar_  las transiciones entre los valores. Como vimos, el proceso de _smoothing_ consistía en un _promediado_, el cual es análogo a la _integración_, por su parte, el proceso de _sharpening_ es análogo a la _derivación_, a este tipo de filtros también se les conoce como _filtros pasa altas_.

En el caso de las señales, la aproximación de la de una derivada de primer orden está dada por las diferencias de valores consecutivos de la señal:

$$\frac{\partial f}{\partial x} = f(x + 1) - f(x)$$

Una señal que tiene la propiedad pasada se muestra a continuación, en donde básicamente se describe la diferencia de dos valores vecinos.

$$w_{dv1} = [-1 \qquad 1]$$

Ahora veamos en la __Figura 9__ el efecto que tiene al realizar la convolución con la ventana $$w_{dv1}$$.

{: .center} 
![ecgSharp1]({{ site.baseurl }}/images/ecg5.PNG)
__Figura 9__ _El utilizar la primera derivada en la señal de ECG, observamos que en aquellas zonas cuyos valores consecutivos son semejantes, la señal de salida se encuentra aproximadamente en cero, en cambio, aquellas regiones en donde la diferencia es más grande muestra una señal con amplitud distinta de cero._

Gracias a esta señal, podemos magnificar las diferencias que existen entre valores vecinos, en donde valores muy semejantes o inluso iguales resultarán en una salida cerca de 0. Por otro lado, la amplitud de la señal de salida será mayor a medida que lo sea la diferencia entre valores consecutivos.

Ahora veamos la segunda derivada, la cual es utilizada para indicar los _cambios de signo_, esta se consigue al derivar nuevamente la primera derivada, es así que tenemos que la derivada de segundo orden se encuentra definida por:

$$\frac{\partial^{2} f}{\partial^{2} x} = f(x + 1) + f(x - 1) - 2f(x)$$

Y la podemos representar mediante la siguiente señal $$w_{dv2}$$:

$$w_{dv2} = [1 \qquad \underline{-2} \qquad 1]$$

Al momento de efectuar la convolución (y de antemano una disculpa si no es muy evidente dado la señal que escogí) notamos que en aquellos valores en donde se encuentra precísamente este cambio de signo (en el complejo QRS), existe un cambio en la señal, en cambio, donde no existe tal cambio los valores serán 0. Como podemos medio observar en la __Figura 10__

{: .center} 
![ecgSharp2]({{ site.baseurl }}/images/ecg6.PNG)
__Figura 10__ _Dado que la frecuencia de muestreo de la señal es grande, la diferencia entre valores consecutivos no es muy evidente, sin embargo, podemos notar que en aquellos puntos críticos más notorios (complejo QRS), existe una respuesta en la señal de salida, en cambio en los demás es cero._

Finalmente llego la hora de aplicar la técnica de _sharpening_ en imágenes, para ello utilizaremos una aproximación del Laplaciano de dos variables, el cual se encuentra definido como:

$$ \nabla^{2}f(x, y) = \frac{\partial^{2} f}{\partial^{2} x} + \frac{\partial^{2} f}{\partial^{2} y}$$

Looks familiar, right? Pues para los cuates es básicamente la unión de las derivadas de segundo orden de $$x$$ y $$y$$, se usan las de segundo orden en lugar de las de primer orden, debido a que es un control más fino al momento de encontrar diferencias entre valores vecinos. Y como vimos en anteriormente, podemos aproximar las segundas derivadas de la siguiente manera:

$$\frac{\partial^{2} f}{\partial^{2} x} = f(x + 1, y) + f(x - 1, y) - 2f(x, y)$$

$$\frac{\partial^{2} f}{\partial^{2} y} = f(x, y + 1) + f(x, y - 1) - 2f(x, y)$$

Por lo tanto, el operador quedaría aproximado de la manera:

$$ \nabla^{2}f(x, y) = f(x + 1, y) + f(x - 1, y) + f(x, y + 1) + f(x, y - 1) - 4f(x, y)$$

Y en formato de matriz, por el filtro $$w_{sharp2D}$$:

$$
w_{sharp2D} = \begin{vmatrix}
0&1&0\\
1&-4&1\\
0&1&0\\
\end{vmatrix}
$$

En la __Figura 11__ encontramos el resultado de la convolución con este filtro, cen ella observamos que las zonas oscuras corresponden a aquellas regiones en donde la diferencia entre vecinos es mínica, por otro lado, las líneas blancas indican los bordes dentro de la imagen, las cuales son originadas por diferencias considerables entre pixeles vecinos.

{: .center} 
![ecgSharp2]({{ site.baseurl }}/images/kernel5.PNG)
__Figura 11__ _Resultado de la convolución con el operador de sharpening $$w_{sharp2d}$$, cuyas líneas blancas se refieren a los bordes en la imagen, en cambio, aquellos con amplitud nula (zonas oscuras) se refieren a aquellas regiones que son parte de una misma región (poca diferencia entre ellos)._

Más adelante veremos más aplicaciones, resultado de aplicar estos filtros de manera conjunta...además de más filtros :)

______

### Referencias
* [libro de gonzalez](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)
* [libro de A. Jain](https://www.amazon.com/Fundamentals-Digital-Image-Processing-Anil/dp/0133361659)
* [video que explica algunos de los filtros espaciales](https://www.youtube.com/watch?v=q9AqlQ274ss)
















