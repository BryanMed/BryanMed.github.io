---
layout: post
comments: true
mathjax: true
title: 2.3| Transformación de Potencia (Corrección gama)
---

Además de la [transformación logarítmica](https://bryanmed.github.io/TransformacionLogaritmo/), existe toda una familia de funciones que se encarga de comprimir/ampliar el rango dinámico del brillo de una imagen. La _transformación de potencia_, se encuentra definida por:

{: .center}
$$g(x, y) = c \: f(x, y)^{\gamma}$$

En donde $$g(x, y)$$ corresponde a la imagen de salida, el valor de $$c$$, por otro lado, es una constante de escalamiento, que nos permite obtener los valores de salida dentro de un rango deseado (en este caso de 0 - 255), la cual es calculada a partir de:

{: .center}
$$c = \frac{255}{\max(f(x, y)^{\gamma}) }$$

La transformación de potencia es conocida también _corrección gamma_ dado que el exponente por el cual será elevado el brillo de la imagen $$f(x, y)$$ está denotado por la constante $$\gamma$$ (gamma), cuyo valor siempre será positivo.

Y bueno, cuando $$\gamma = 1$$ los valores de los pixeles serán elevados a 1, y por tanto, no tendrá ningún efecto a la salida. No obstante, cuando los valores de $$\gamma$$ son menores a la unidad, se obtiene un efecto similar al de la transformación logaritmo, en donde a las regiones oscuras se les asigna un mayor rango dinámico en la salida, mejorando el contraste en estas zonas. Por otro lado, con valores de $$\gamma$$ mayores a la unidad, pasa exactamente lo contrario, las regiones de brillos intensos son mapeados a un rango de grises más amplio, mejorando el nivel de detalle. En la __Figura 2.1__ observamos en la gráfica, la morfología que adoptan las funciones de mapeo de acuerdo al valor de $$\gamma$$ asignado, y enseguida podemos notar el efecto que tienen estas transformaciones en la imagen.   

{: .center}
![gammagraph]({{ site.baseurl }}/images/graphGamma.PNG)
![gammaLenna]({{ site.baseurl }}/images/gamaLena.PNG)
 __Figura 2.1__ _babaababa_.


{: .center}
![espinazo]({{ site.baseurl }}/images/gammaEspinazo.PNG)

{: .center}
![rose]({{ site.baseurl }}/images/gammaRose.PNG)




http://drosehoops.com/2018/08/derrick-rose-announces-the-rose-scholars-program/
https://radiopaedia.org/cases/ganglioglioma-of-the-cervical-cord
