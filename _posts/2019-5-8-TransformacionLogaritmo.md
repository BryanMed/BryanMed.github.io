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
$$c = \frac{255}{\log(1 + \max(f(x, y)}$$





https://es.khanacademy.org/math/algebra2/exponential-and-logarithmic-functions/introduction-to-logarithms/a/intro-to-logarithms




