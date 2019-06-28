---
layout: post
comments: true
mathjax: true
title: 3| Convolución (Filtrado espacial)
--- 

LLegó el momento de hablar de la convolución, esta es una herramienta primordial en el procesamiento digital de imágenes, visión computacional, e incluso es un pilar importante en el machine learning. Una de las dudas frecuentes, es la confusión que existe entre convolución y correlación. Pues bien, ambos procesos son muy similares, de hecho, la única diferencia es que en la convolución una señal está invertida, pero esto es suficiente para generar aplicaciones un tanto diferentes, de tal manera que:

* __La correlación__ es utilizada para medir el grado de __similitud__ entre dos señales.
* __la convolución__ en cambio, sirve para conocer el efecto de una señal respecto a la otra.

Para fines prácticos me limitaré a explicar en este post únicamente la convolución. Y bueno, la __convolución__ _discreta_ en 1D de dos señales $$x$$ y $$h$$, estando representada por el operador __*__, con lo cual se define de la siguiente manera:

{: .center}
$$y[n] = (x[n] * h[n]) = \sum_{k = -\infty}^{\infty} x[k]h[n - k]$$

Veamos como se realiza el proceso que se indica en la operación de arriba, en el siguiente _combo-cuates_:

* __Reflexión__: Se refleja $$h(k)$$, obteniendo así $$h[-k]$$
* __Desplazamiento__: Ahora $$h(-k)$$ se desplaza en un instante de tiempo $$n_0$$, resultando en $$h[n_0 - k]$$
* __Multiplicación__: Esta vez se multiplican las señales $$x[k]$$ y $$h[n_0 - k]$$, obteniendo una secuencia de valores.  
* __Suma__: Finalmente se suman los valores de la secuencia anterior, siendo esta sumatoria el resultado de la convolución (la señal de salida $$y[n]$$) en el instante en el que $$n = n_0$$.

_____
Ahora veamos un ejemplo práctico de la convolución en 1D. Consideramos las señales $$x = [1, 2, 3]$$ y  $$h = [1, 2]$$. 

{: .center}
![conv1d1]({{ site.baseurl }}/images/conv1d1.PNG)

Estas señales serán puestas en función de $$k$$, así, en el caso de $$x[n]$$ simplemente realizamos un cambio de variable, obteniendo $$x[k]$$, por otro lado, $$h[n]$$ se convertirá en primera instancia a $$h[-k]$$ lo cual invierte el sentido de la señal, para acto seguido, desplazar esta señal arbitrariamente $$n$$ veces, en la siguiente figura consideramos a $$n < 0$$.

{: .center}
![conv1d2]({{ site.baseurl }}/images/conv1d2.PNG)

Ahora realizaremos el proceso de convolución, el primer elemento de interés de la convolución es aquel en donde empiezan a _sobreponerse_, en este caso, cuando $$n = 0$$, así, $$y[0]$$ es igual a la suma de los productos de aquellos elementos que se "traslapan" (se muestran en rojo). Por cierto, se agregan los 0s necesarios en la señal $$x[k]$$ para poder realizar las multiplicaciones, cuando no se traslapan. 

{: .center}
![conv1d3]({{ site.baseurl }}/images/conv1d3.PNG)

Esta vez, consideramos a $$n = 1$$ con lo cual la respuesta al impulso $$h[n - k]$$ es deplazada un elemento ($$h[1-k]$$), ahora los elementos 1 y 2 de ambas señales son las que se superponen, con lo cual se realiza la multiplicación de los elementos correspondientes (para el elemento 1: 1 x 2; para el elemento 2: 2 x 1), siendo la salida de la convolución $$y[1] = 1 \times 2 + 2 \times 1 = 4$$.

{: .center}
![conv1d4]({{ site.baseurl }}/images/conv1d4.PNG)

Para el caso de $$n = 2$$ se realiza un desplazamiento de 2 unidades respecto a la señal original, siendo los elementos 2 y 3 los que se sobreponen, por lo que al realizar este proceso, tenemos que $$y[2] = 2 \times 2 + 3 \times 1 = 7$$.

{: .center}
![conv1d5]({{ site.baseurl }}/images/conv1d5.PNG)

Finalmente, se desplaza nuevamente la señal en $$n = 3$$, esta vez la función $$h[3 - k]$$ ya va de salida, con lo cual solo coinciden ambas señales en el elemento 2, obteniendo $$y[3] = 3 \times 2 = 6$$

{: .center}
![conv1d6]({{ site.baseurl }}/images/conv1d6.PNG)

El resultado de la convolución se muestra a continuación, obviamente no se toman en cuenta aquellos elementos en donde $$x[n]$$ y $$h[n]$$ no se sobreponen.

{: .center}
![conv1d6]({{ site.baseurl }}/images/conv1d6.PNG)

Con esto ya estamos listos para dar el salto a la convolución en 2D :)

