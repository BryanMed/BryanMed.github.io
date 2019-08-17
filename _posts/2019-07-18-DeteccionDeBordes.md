---
layout: post
comments: true
mathjax: true
title: PDI-4.1| Detección de Bordes - Tipos de bordes
--- 
Los _bordes (edges)_  son identificados como el límite que separa dos regiones dentro de una imagen. El objetivo de la detección de bordes es el de reducir en gran medida la cantidad de datos, al preservar únicamente la información concerniente a lo que delimita las estructuras, como observamos en la __Figura 1__, donde a la izquierda encontramos la imagen original y a la derecha únicamente los bordes de esta, esta operación es de vital importancia en áreas como reconocimiento de patrones y aprendizaje automático, entre otras.

{: .center} 
![jordan]({{ site.baseurl }}/images/jordan.PNG)
__Figura 1__ _A la izquierda se encuentra el logo Jordan "Jumpman", a la derecha solamente el borde que define a esta estructura. Notamos que la información de la imagen quedó reducida únicamente a unos cientos de pixeles_.

Entre las distintas características que existen para detectar los bordes, en este post trataremos unicamente los referentes a la variación de intensidad. Los bordes se forman a partir de _cambios abruptos_ (otros no tanto) del nivel de brillo, estos se clasifican de acuerdo a su perfil de intensidad de la siguiente manera:

* __Step edges__: Se encuentran en zonas donde existe un cambio súbito de intensidad (idealmente de un pixel a otro). Con lo cual estos bordes son modelados como una funcion de escalón unitario. Este es el borde ideal, sin embargo es poco usual encontrarlo en imágenes no artificales.

* __Ramp edges__: Estos se producen cuando el cambio de brillo no es instantáneo, si no que existe una ventana de tiempo en la que va variando hasta alcanzar la nueva intensidad. La función que la representa es precisamente la función rampa. Son de los más comunes de encontrar, dado que en la gran mayoría de imágenes encontramos ya sea ruido, o desenfoques que producen cierto suavizado en regiones, lo cual produce una transición más _smooth_ entre las regiones, resultando en una transición más lenta (asemejandose a la función rampa).

* __Roof edges__: Se encuentran cuando existe una doble transición de intensidades en un periodo relativamente corto de tiempo, normalmente es generado por líneas.

En la __Figura 2__ encontramos los 3 casos de bordes. En el primer renglón encontramos los bordes como los encontramos dentro de una imagen, en el segundo renglón vemos los perfiles de intensidad, en donde visualizamos a las intensidades como una superficie, donde la altura máxima corresponde al brillo total (1 ya que estamos trabajando con imágenes tipo _float_) y 0 para la auscencia de este. Finalmente, en el tercer renglón vemos como se modelan los bordes mediante señales.

{: .center} 
![levels]({{ site.baseurl }}/images/levels.PNG)
__Figura 2__ _En el renglón superior encontramos los distintos bordes que podemos encontrar en una imagen, en el renglón central observamos la representación 3D, en donde la altura está determinada por el nivel de intensidad, finalmente encontramos la manera en la que se encuentran modeladas estas señales_.

> El código para visualizar los bordes en Python, lo puedes encontrar [aquí](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/4.1%20visualizador%20de%20bordes).

En la vida real, encontramos aproximaciones a este tipo de bordes como en la __Figura 3__, es por ello que las técnicas que hablaremos en la siguiente entrada van encaminadas a utilizar estas propiedades a fin de encontrarlos.

{: .center} 
![uaslpBordes]({{ site.baseurl }}/images/uaslpBordes.PNG)
__Figura 3__ _Edificio central de la UASLP, donde podemos identificar los tipos de bordes mencionados anteriormente_.

_____

### Referencias

* [libro de Gonzalez](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)
* https://www.cse.unr.edu/~bebis/CS791E/Notes/EdgeDetection.pdf
* [libro de A. Jain](https://www.amazon.com/Fundamentals-Digital-Image-Processing-Anil/dp/0133361659)







