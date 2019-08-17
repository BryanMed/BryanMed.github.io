---
layout: post
comments: true
mathjax: true
title: PDI-2.2| Transformación logaritmo
---
Y si, como el título lo indica, aplicaremos el logaritmo a cada uno de los pixeles de la imagen, pero antes de llegar a esa parte refresquemos un poquito, ¿qué es un _logaritmo_?

## Logaritmo

Bien, en la [wiki](https://es.wikipedia.org/wiki/Logaritmo) encontramos que el logaritmo está definido como:
>"Dado un número real (argumento $$x$$), la función logaritmo le asigna el exponente $$n$$ (o potencia) a la que un número fijo $$b$$ (base) se ha de elevar para obtener dicho argumento."

>$$\log_{b}x = n$$

Algo chispa, ¿no? pero tranqui, como sabemos la suma es la operación opuesta a la resta, y la multiplicación lo es para la división. El logaritmo surge como la función antagónica a la _exponenciación_. 
Por ejemplo, el resultado de elevar $$2$$ a la $$3^{a}$$ potencia ($$2^{3}$$) da como resultado $$8$$, esto lo interpretamos como el _número de veces_ (3) por el cual se debe multplicar el 2 por sí mismo, es decir:

{: .center} 
$$2^{3} = 2 \times 2 \times 2 = 8$$

En el logaritmo nos preguntamos ¿a qué potencia debemos de elevar la base ($$2$$) para obtener $$8$$? y... pues sí, $$3$$

$$2^{3} = 8 \longleftrightarrow \log_{2}8 = 3$$

* Ojito que el logaritmo solo está definido para número reales positivos ($$>0$$).

> La implementación de este algoritmo en Python y Matlab la encuentras en [este](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/2.2%20logaritmo) repositorio.

Y bueno, después de esa breve introducción, ahora si entraremos en materia, el logaritmo es utilizado como función de transformación con el objetivo de ampliar el rango dinámico de ciertas intensidades, teniendo claro, el compromiso de reducirlo en otras. Este método está definido por:

{: .center}
$$g(x, y) = c \: \log(1 + f(x, y)$$

En este caso, el $$1$$ dentro de la función es necesario ya que, como mencionamos antes, el logaritmo no está definido en $$0$$ y es muy (pero que muy) seguro encontrar pixeles con nivel de intensidad igual a $$0$$. Por otro lado, el valor de la constante $$c$$ está definido por:

{: .center}
$$c = \frac{255}{\log(1 + \max(f(x, y)))}$$

El propósito de esta constante es el de ajustar el rango de valores de salida a un rango apropiado para su despliegue en pantalla (8 bits), con ello, la máxima intensidad que se podrá obtener gracias a esta constante de _escalamiento_ será de 255. En la __Figura 2.1__ observamos la manera en la que la función _mapea_ las intensidades.

{: .center}
![logVS]({{ site.baseurl }}/images/logVS.PNG)
 __Figura 2.1__ _En este caso, al tener una intensidad de 200 en la entrada, obtenemos a la salida una intensidad de 243 _.

Una de las mayores aplicaciones de esta transformación es la _comprimir_ el rango dinámico de las imágenes obtenidas por la _transformada de Fourier_ (ya veremos este temita más adelante) en donde las intensidades se pueden encontrar en un rango de $$0$$ hasta $$10^{6}$$ (incluso más). ¿Cual es el problema con el despliegue de estas imágenes? Pues que en el caso de hacer simplemente una relación lineal entre el rango de la imagen de entrada ($$[0 - 10^{6}]$$) para su despliegue en un dispositivo de 8 bits (rango de $$[0 - 255]$$), los valores con mayor intensidad en la entrada, serán considerados blancos en la salida, sin embargo, estos pixeles acapararán toda la atención, y los detalles que ofrecen los pobres pixeles con brillos intermedios y oscuros serán mayormenente ignorados ya que las intensidades que les son asignadas a la salida serán muy similares entre sí, por ejemplo una diferencia de quizá 1000 unidades en la entrada, será igual o menor a una diferencia unitaria en la salida (yup, indeferenciable al ojo humano). Lo que nos permite la transformación logarítmica es, precisamente, _ampliar_ el rango de despliegue de aquellas intensidades bajas y oscuras. En la __Figura 2.2__ encontramos un ejemplo de los efectos de esta transformación en una imagen del espectro de Fourier.

{: .center}
![logFourier]({{ site.baseurl }}/images/logF1.PNG)
 __Figura 2.2__ _Se observa la gran mejora en la imagen, que nos permite apreciar con más claridad aquellos detalles que antes de la transformada, estaban ocultos (la imagen la tomé de [aquí](http://www.cs.uregina.ca/Links/class-info/425-nova/Lab5/index.html
)_.

Y bueno, en la __Figura 2.3__ encontramos otro ejemplito en donde se amplia el rango de las intensidades grisáceas.

{: .center}
![logDark]({{ site.baseurl }}/images/logDark.PNG)
 __Figura 2.3__ _Se observa un mayor __contraste__ en la imagen de salida_ ... imagen tomada de la [serie Dark de Netflix](https://www.netflix.com/mx/title/80100172).
 
 Pero esta transformación no siempre es adecuada, como vemos, en la __Figura 2.4__, en el que pareciera que le aplicamos un _offset_ a la imagen, saturandola de intensidades altas.

{: .center}
![logLena]({{ site.baseurl }}/images/logLena.PNG)
 __Figura 2.4__ _Poco contraste en la imagen resultante_.


  

## Referencias

* [explicación de logaritmo wiki](https://es.wikipedia.org/wiki/Logaritmo)
* [explicación de logaritmo Khanacademy](https://es.khanacademy.org/math/algebra2/exponential-and-logarithmic-functions/introduction-to-logarithms/a/intro-to-logarithms)
* [libro de Digital Image Processing de Gonzalez & Woods](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)
* [buenísima explicación del logaritmo en image processing](https://homepages.inf.ed.ac.uk/rbf/HIPR2/pixlog.htm)



