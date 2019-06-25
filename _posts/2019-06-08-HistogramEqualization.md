---
layout: post
comments: true
mathjax: true
title: 2.6| Ecualización de Histograma
---

Tomémonos un tiempo para analizar y discutir los siguientes histogramas (con su respectiva imagen). En el primer caso, que se muestra en la __Figura 1__ observamos que la distribución del histograma está concentrada en los valores bajos de intensidad, esto a su vez se ve reflejado en la imagen correspondiente, la cual es predominantemente oscura, y con un bajísimo contraste. 

{: .center}
![zorroOscuro]({{ site.baseurl }}/images/gamaLena.PNG)
__Figura 1__ _ayura_.

Caso contrario en la __Figura 2__, en la que sí, seguimos observando una distribucióm concentrada, pero en este caso en los valores de intensidades altas. Esto nos indica que la imagen está saturada en los valores altos, presentando poco contraste.

{: .center}
![zorroClaro]({{ site.baseurl }}/images/gamaLena.PNG)
__Figura 2__ _ayura_.

Finalmente, la __Figura 3__ corresponde a la imagen original, y podemos notar que se tiene un mayor contraste respecto a los casos anteriores, debido a que la distribución abarca la gran mayoria de los niveles de brillo.

{: .center}
![zorroNormie]({{ site.baseurl }}/images/gamaLena.PNG)
__Figura 3__ _ayura_.

No obstante, aún es posible mejorar el contraste de esta imagen. Podemos pensar en utilizar la técnica anteriormente discutida de [contrast stretching](https://bryanmed.github.io/LinearTrans/), sin embargo, su función es precisamente ampliar el rango dinámico, y en este caso eso ya no es un problema. Una técnica que se puede utilizar es la llamada _Ecualización del histograma_, la cual tiene como objetivo mejorar el contraste de una imagen, al generar una _distribución uniforme_ de las intensidades de salida, esto se ejemplifica en el diagrama de la __Figura 4__.

{: .center}
![zorroNormie]({{ site.baseurl }}/images/gamaLena.PNG)
__Figura 4__ _ayura_.

Para demostrar esto, consideremos el caso continuo, en donde las función de transformación se encuentra de la forma:

{: .center}
$$s = T(r), r \in [0, L - 1]$$

En donde $$s$$ es la imagen de salida, $$T$$ es la función de transformación y $$r$$ es la imagen de entrada. Para realizar este método se toma en cuenta una sola consideración y es que:

* $$T(r)$$ sea _monotónicamente creciente_ en el mismo intérvalo ($$ r \in [L - 1]$$).

Esto nos garantiza que la función de transformación vaya de 0 a 255, y que se evite retrocesos de intensidad. Ahora, podemos tomar los niveles de gris de ambas imágenes como funciones de probabilidad. En este caso en particular $$P_{r}(r)$$ como la función de densidad de probabilidad de $$r$$, y $$P_{s}(s)$$ para $$s$$. Entonces, al garantizar que $$T(r)$$ es continua y diferenciable, podemos calcular $$P_{s}(s)$$, como:

{: .center}
$$P_{s}(s) = P_{r}(r) \dot |\frac{dr}{ds}|$$

Una función que cumple con el enunciado de ser monotónicamente creciente, es la función de densidad acumulada, de la forma:

{: .center}
$$s = T(r) = (L-1) \int_{0}^{r} P_{r}(w) dw$$

Así, al diferenciar respecto a $$r$$, la ecuación $$s = T(r)$$, tenemos: 

{: .center}
$$\frac{ds}{dr} = \frac{dT(r)}{ds}$$

$$\frac{ds}{dr} = (L-1) \frac{dP_{r}(r) \dot |\frac{dr}{ds}|}{dr}$$

$$\frac{ds}{dr} = (L-1) P_{r}(r)$$

Con esto, sustituimos $$\frac{ds}{dr}$$ en la primera ecuación, de tal manera que:

{: .center}
$$P_{s}(s) = P_{r}(r) \dot |\frac{dr}{ds}|$$

$$P_{s}(s) = P_{r}(r) \dot |frac{1}{(L-1)P_{r}(r)}|$$

$$P_{s}(s) = frac{1}{(L-1)P_{r}(r)}$$

Con lo cual, se concluye que la distribución será un valor constante, independientemente del valor de entrada (y tendra una distribución uniforme -> equiprobable)



