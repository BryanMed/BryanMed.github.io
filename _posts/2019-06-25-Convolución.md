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

Estas señales serán puestas en función de $$k$$, así, en el caso de $$x[n]$$ simplemente realizamos un cambio de variable, obteniendo $$x[k]$$, por otro lado, $$h[n]$$ se convertirá en primera instancia a $$h[-k]$$ lo cual invierte el sentido de la señal, para acto seguido, desplazar esta señal arbitrariamente $$n$$ veces.
