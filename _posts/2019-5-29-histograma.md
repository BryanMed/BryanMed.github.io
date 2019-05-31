---
layout: post
comments: true
mathjax: true
title: 2.4| Histograma 
---

El _Histograma_ es una buena caracterización inicial de una imagen, nos permite observar de manera sencilla la distribución de las intensidades que tiene una imagen en particular, y con esto, diseñar una estrategia para mejorarla.

Se encuentra definido como una función unidimensional discreta, de la forma:

{: .center}
$$H[r] = n$$

En donde la variable independiente $$r$$ corresponde a los niveles de brillo de la imagen (en el histograma se les nombra usualmente como bins). Por otro lado, la variable dependiente $$n$$ indica el número de pixeles que cuentan con esa intensidad. Consideremos el caso que se observa en la __Figura 2.1__, en la cual contamos con una imagen de tamaño 5 x 5 (25 pixeles), con dos niveles de intensidad (0 para las casillas oscuras, 1 para las oscuras). El histograma de esta imagen en particular se muestra a la derecha, cuya altura de cada columna indica la cantidad de pixeles con ese nivel de intensidad.

{: .center}
![5x5]({{ site.baseurl }}/images/Histograma5x5.PNG)
__Figura 2.1__ _A la izquierda se muestra una imagen de 5x5, en donde 5 pixeles corresponden al color oscuro y 20 al blanco. A la derecha se muestra su histograma, con el cual podemos observar rápidamente la cantidad de pixeles correspondientes a cada intensidad._

Muchas veces el histograma es _normalizado_, es decir, que los componentes $$n$$ son divididos por el número total de pixeles ($$N$$) de la imagen, con lo cual se tiene:

{: .center}
$$H[r] = \frac{n}{N}$$

Y cuya suma de todos los componentes resulta en la unidad. A esta representación se le conoce como la función de densidad de probabilidad de una imagen, en donde se nos muestra la probabilidad (en una escala de 0 a 1) de encontrar un pixel en particular con determinado brillo dentro de la imagen.

> La implementación del Histograma de una imagen  (Python y MATLAB) la encuentras en [este](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/2.5%20Histograma) repositorio.

Como mencionamos en un inicio, el histograma es muy útil para caracterizar una imagen, por ejemplo, en la __Figura 2.2__ observamos la manera en la que el histograma cambia de acuerdo a las intensidades que se presentan. La primera imagen está saturada con altos niveles de brillo , es por ello que en el histograma correspondiente observamos que las intensidades altas son las que predominan. Por otro lado, en la imagen oscura, vemos como la distribución del histograma se concentra en los niveles bajos. Una imagen que exhibe un mayor contraste, es aquella que cuenta con una distribución mas amplia de intensidades

{: .center}
![lightHist]({{ site.baseurl }}/images/HistLight.PNG)

![DarkHist]({{ site.baseurl }}/images/HistDark.PNG)

![NormHist]({{ site.baseurl }}/images/HistNorm.PNG)
__Figura 2.2__ _En la imagen superior se obsera una imagen saturada en altas intensidades, en medio encontramos una imagen predominantemente oscura y finalmente una imagen en donde se aprecian mejor los detalles; a un lado, encontramos su respectivo de histograma que nos da una idea de la distribución de los niveles de brillo de la imagen._

En la __Figura 2.3__ observamos otro ejemplo de la importancia que tienen los histogramas a la hora de mejorar el proceso de comprensión de la información en una imagen. Recordando la [Transformación Negativa](https://bryanmed.github.io/ImagenNegativa/), en donde se obtiene el inverso de una imagen, al observar sus histogramas notamos que este último también es invertido. 

{: .center}
![negHist]({{ site.baseurl }}/images/HistInverse.PNG)
__Figura 2.3__ _La imagen negativa se forma al sustituir el valor de intensidad original por su complemento, en este caso, el histograma refleja este mismo hecho._

## Referencias
* [Libro de Digital Image Processing de Gonzalez y Woods](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)

* [Notas de fundamentos de DIP - Roger L. Easton jr.] (https://www.cis.rit.edu/class/simg361/Notes_11222010.pdf)




