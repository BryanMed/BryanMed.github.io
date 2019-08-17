---
layout: post
comments: true
mathjax: true
title: PDI-2.3| Transformación de Potencia (Corrección gama)
---

Además de la [transformación logarítmica](https://bryanmed.github.io/TransformacionLogaritmo/), existe toda una familia de funciones que se encarga de comprimir/ampliar el rango dinámico del brillo de una imagen. La _transformación de potencia_, se encuentra definida por:

{: .center}
$$g(x, y) = c \: f(x, y)^{\gamma}$$

En donde $$g(x, y)$$ corresponde a la imagen de salida, el valor de $$c$$, por otro lado, es una constante de escalamiento que nos permite obtener los valores de salida dentro de un rango deseado (en este caso de 0 - 255), la cual es calculada a partir de:

{: .center}
$$c = \frac{255}{\max(f(x, y)^{\gamma}) }$$

La transformación de potencia es conocida también _corrección gamma_ dado que el exponente por el cual será elevado el brillo de la imagen $$f(x, y)$$ está denotado por la constante $$\gamma$$ (gamma), cuyo valor siempre será positivo.

Y bueno, cuando $$\gamma = 1$$ los valores de los pixeles serán elevados a 1, y por tanto, no tendrá ningún efecto a la salida. No obstante, cuando los valores de $$\gamma$$ son menores a la unidad, se obtiene un efecto similar al de la transformación logaritmo, en donde a las regiones oscuras se les asigna un mayor rango dinámico en la salida, mejorando el contraste en estas zonas con poca iluminación. Por otro lado, con valores de $$\gamma$$ mayores a la unidad, pasa exactamente lo contrario, las regiones de brillos intensos son mapeados a un rango de grises más amplio, mejorando la diferenciación de detalles en zonas brillosas. En la __Figura 2.1__ observamos en la gráfica, la morfología que adoptan las funciones de mapeo de acuerdo al valor de $$\gamma$$ asignado, y enseguida podemos notar el efecto que tienen estas transformaciones en la imagen.   


{: .center}
![gammaLenna]({{ site.baseurl }}/images/gamaLena.PNG)
![gammagraph]({{ site.baseurl }}/images/graphGamma.PNG)
__Figura 2.1__ _Observamos el efecto que tienen algunos valores de $$\gamma$$, en donde tomamos como ejemplo un nivel de intensidad de 200 en la entrada, cuando $$\gamma = 0.4$$ la transformación adopta la forma mostrada en la función de color azul, en donde en la salida se obtiene una intensidad de 231. Cuando $$\gamma = 2.5$$ (función en amarillo), el nivel de intensidad que se obtiene con la misma entrada será de 138_.

> La implementación de este algoritmo en Python y Matlab la encuentras en [este](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/2.3%20correccion%20gamma) repositorio.

A continuación, veremos dos casos en donde mediante el uso de la transformación de potencia, se logra mejorar el nivel de detalle en las imágenes, en el caso de la __Figura 2.2__, observamos que es una imagen con grandes regiones oscuras, así que, si aplicamos la corrección gamma, con $$\gamma < 1$$ podemos esperar que se logre visualizar de mejor manera estas regiones.

{: .center}
![espinazo]({{ site.baseurl }}/images/gammaEspinazo.PNG)
__Figura 2.2__ _Cuando se utiliza una $$\gamma <1$$ las regiones oscuras son mapeadas a un rango mayor de intensidades, por lo que se mejora el constraste en estas zonas. Podemos corroborar este hecho al observar la imagen de la izquierda, en donde aparece información que no era percibida en la imagen original (al centro), en cambio, el hecho de aplicar una $$\gamma >1$$ no es beneficioso para la visualización ... imagen de una lesión de la [médula espinal](https://radiopaedia.org/cases/ganglioglioma-of-the-cervical-cord)_.


Por otro lado, al utilizar una $$\gamma > 1$$ podemos mejorar la percepción de información cuando nos encontramos con zonas muy brillosas, asignandoles un mayor rango, haciendo más evidente las diferencias entre valores con brillo alto, como el ejemplo mostrado en la __Figura 2.3__.


{: .center}
![rose]({{ site.baseurl }}/images/gammaRose.PNG)
__Figura 2.3__ _Al utilizar una $$\gamma > 1$$ observamos que algunas zonas brillosas de la imagen son mejor percibidas, respecto a cuando utilizamos la imagen con una $$\gamma \leq 1$$ ... imagen de [Derrick Rose](http://drosehoops.com/2018/08/derrick-rose-announces-the-rose-scholars-program/)_.


## Referencias
 
* [capitulo 3 del libro de Gonzalez](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)
* [capitulo 5 del libro Digital Image Processing for medical applications](https://www.cambridge.org/mx/academic/subjects/engineering/biomedical-engineering/digital-image-processing-medical-applications?format=HB&isbn=9780521860857)
* [explicación del operador exponencial/potencia](https://homepages.inf.ed.ac.uk/rbf/HIPR2/pixexp.htm)
