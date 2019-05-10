---
layout: post
comments: true
mathjax: true
title: 2.2| Transformación logaritmo
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

Y bueno, después de esa breve introducción, ahora si entraremos en materia, el logaritmo es utilizado como función de transformación con el objetivo de ampliar el rango dinámico de ciertas intensidades, teniendo claro, el compromiso de reducirlo en otras. Este método está definido por:

{: .center}
$$g(x, y) = c \: \log(1 + f(x, y)$$

En este caso, el $$1$$ dentro de la función es necesario ya que, como mencionamos antes, el logaritmo no está definido en $$0$$ y es muy (pero que muy) seguro encontrar pixeles con nivel de intensidad igual a $$0$$. Por otro lado, el valor de la constante $$c$$ está definido por:

{: .center}
$$c = \frac{255}{\log(1 + \max(f(x, y)))}$$

El propósito de esta constante es el de ajustar el rango de valores de salida a un rango apropiado para su despliegue en pantalla (8 bits), con ello, la máxima intensidad que se podrá obtener gracias a esta constante de _escalamiento_ será de 255.

Una de las mayores aplicaciones de esta transformación es la _comprimir_ el rango dinámico de las imágenes obtenidas por la _transformada de Fourier_ (ya veremos este temita más adelante) en donde las intensidades se pueden encontrar en un rango de $$0$$ hasta $$10^{6}$$ (incluso más). ¿Cual es el problema con el despliegue de estas imágenes? Pues que en el caso de hacer simplemente una relación lineal entre el rango de la imagen de entrada ($$[0 - 10^{6}]$$) para su despliegue en un dispositivo de 8 bits (rango de $$[0 - 255]$$), los valores con mayor intensidad en la entrada, serán considerados blancos en la salida, sin embargo, estos pixeles acapararán toda la atención, y los detalles que ofrecen los pobres pixeles con brillos intermedios y oscuros serán mayormenente ignorados ya que las intensidades que les son asignadas a la salida serán muy similares entre sí, por ejemplo una diferencia de quizá 1000 unidades en la entrada, será igual o menor a una diferencia unitaria en la salida (yup, indeferenciable al ojo humano). Lo que nos permite la transformación logarítmica es, precisamente, _ampliar_ el rango de despliegue de aquellas intensidades bajas y oscuras. En la __Figura 2.1__ encontramos un ejemplo de los efectos de esta transformación en una imagen del espectro de Fourier.

ignorados, ya que no es posb

serán considerados como blancos, pero a su vez, las intensidades intermedias o bajas serán prácticamente imperceptibles, perdiendo  



https://es.khanacademy.org/math/algebra2/exponential-and-logarithmic-functions/introduction-to-logarithms/a/intro-to-logarithms




