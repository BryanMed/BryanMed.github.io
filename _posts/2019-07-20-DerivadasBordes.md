---
layout: post
comments: true
mathjax: true
title: 4.2| Detección de Bordes - Derivadas
--- 
En este post explicaremos el papel que juega la convolución y las derivadas en la detección de bordes. Para fines prácticos y de visualización, usaremos el modelo "ideal" de _impulso unitario_ el cual es el modelado de un borde muy "sharp" (transición de intensidad muy abrupta).

Y bueno, para detectar bordes la herramienta predilecta es _la [convolución](https://bryanmed.github.io/kernelsConv/)_, en donde básicamente hacemos pasar un kernel por toda la imagen, y por cada pixel de esta obtendremos una respuesta que es dependiente tanto de los valores del kernel, así como de la vecindad del pixel correspondiente.

Bien, entonces ya sabemos que un borde es una transición de intensidad en un tiempo relativamente corto de tiempo, y que para detectarlos usamos la convolución, pero, ¿qué características buscamos en un _edge detector_?... principalmente dos: 

* Que en las zonas de brillo uniforme (donde no existen cambios tan grandes de intensidad) la respuesta del detector sea mínima. "Pues aquí no hay nada men, todo tranqui".

* Por otro lado, en la zonas donde existe un cambio "abrupto" de intensidad, la respuesta del detector debe ser grande (y por respuesta me refiero al valor resultante de la convolución), que nos indique "épale men, here´s something".

Es ahora cuando viene la pregunta ¿Existirá algo que permita generar este tipo de respuestas tan específicas?. Aquí es cuando entran en juego las _derivadas_ que, long story short, son las _diferencias_ entre valores consecutivos, el qué tanto cambió el valor actual respecto al valor pasado. Tomemos como ejemplo el renglón de pixeles de la __Figura 1__.

{: .center} 
![stepEdge]({{ site.baseurl }}/images/stepEdge.PNG)
__Figura 1__ _Encontramos un renglón de pixeles correspondientes a una imagen, en donde existe una transición de intensidad en los pixeles 25-26 (step edge)_.

Como podemos observar, la transición de intensidad se da entre los pixeles 25-26 (pixel 25 = 0, pixel 26 = 1). Esto representado como señal se modela como una función unidimensional de impulso unitario, con punto de quiebre en los valores 25-26, mostrado en la __Figura 2__.

{: .center} 
![stepEdge]({{ site.baseurl }}/images/funcionImpulso.png)
__Figura 2__ _El modelado de la función correspondiente a la figura anterior, en donde pasamos del mínimo al máximo brillo en los elementos 25-26_.

Ahora recomiendo mucho leer la sección de _operadores de sharpening_ del post de [convolución](https://bryanmed.github.io/kernelsConv/) ya que ahí explico un poquito el transfondo del kernel de derivada. Resumiendo un poquito, la derivada de una señal $$f$$ se puede aproximar como las diferencias de valores consecutivos, de la forma:

$$f'(x) = f(x + 1) - f(x)$$

Como podemos notar, al valor pasado $$f(x + 1)$$ (recuerda que en una señal el "x + 1" indica un retraso en la señal de 1 unidad) le estamos restando el valor actual $$f(x)$$, es por ello que podemos representar esta señal con el kernel de convolución siguiente:

$$w_{dv1} = [-1 \qquad 1]$$

La versión de este kernel que que utilizaremos, el cual permite que el resultado de la convolución esté centrado en x, es:

$$w_{dv1} = [-1 \qquad \underline{0} \qquad 1]$$

En la __Figura 3__ mostramos lo que sucede cuando realizamos la convolución de la señal escalón, con el kernel de la primera derivada.

{: .center} 
![stepEdge]({{ site.baseurl }}/images/derivadaImpulso.png)
__Figura 3__ _El resultado de realizar la convolución con la máscara de primera derivada, podemos ver que la amplitud 0 corresponde a aquellas regiones sin transiciones de la función impulso, en cambio, en la zona de cambio existe una respuesta de -1, indicando un edge.

Seguramente estarás de "... Bryan, ¿Qué onda con esa señal?, no me dice nada". Tranquilo pequeño saltamontes, recordemos las dos propiedades que buscamos en un detector de bordes, el primero es que cuando fuese una zona donde no existan cambios de intensidad, el detector debe arrojar una respuesta pequeña, como notamos en la señal del anterior, vemos que precisamente la respuesta en las zonas uniformes (regiones posteriores y anteriores a la transición 25-26) es de 0. Segundo, que cuando exista una transición, el detector debe arrojar una magnitud relativamente grande, y oh sorpresa, vemos que el valor de la transición es de -1.

Pero, ¡aún hay más!, ¿qué tal si tratamos con la segunda derivada?, de nuevo, en el post de convolución explicamos como partiendo de la definición de la segunda derivada:

$$f''(x) = f(x + 1) + f(x - 1) - 2f(x)$$

obtenemos el kernel correspondiente:

$$w_{dv2} = [1 \qquad \underline{-2} \qquad 1]$$

El efecto que produce el convolucionar la función escalón con el filtro $$w_{dv2}$$ se muestra en la __Figura 4__ mostrada a continuación.

{: .center} 
![stepEdge]({{ site.baseurl }}/images/2derivadaImpulso.png)
__Figura 4__ _Ahora vemos el resultado de la segunda derivada, notamos que es más escándalosa que la primera derivada, generando dos respuestas por cada borde_.

Como podemos ver, el detector utilizando la 2da derivada es un poquito más sensible a identificar los bordes. Nos produce una doble respuesta: una positiva y otra negativa, pasando en el camino por cero (lo que se conoce como _zero crossing_). Las segundas derivadas tienden a generar bordes más delgados que aquellos producidos por las primera derivada. Además posee otra propiedad importante, con el signo podemos conocer el estado de transición del borde (cuando tenemos un signo negativo, indica que la transición del borde va de blanco a negro. Con signo positivo corresponde a un cambio de oscuro a blanco).

En el siguiente post veremos ahora si imágenes :)

____

### Referencias

* [libro de Gonzalez](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)
* https://www.cse.unr.edu/~bebis/CS791E/Notes/EdgeDetection.pdf
* [libro de A. Jain](https://www.amazon.com/Fundamentals-Digital-Image-Processing-Anil/dp/0133361659)




















