---
layout: post
comments: true
mathjax: true
title: 2.4| Transformacion lineal por partes (contrast stretching)
---

Las transformaciones que modifican los niveles de intensidad de una imagen no tienen porqué estar limitados a funciones matemáticas bien definidas, como la [Transformación logaritmo](https://bryanmed.github.io/TransformacionLogaritmo/) o [Transformación gamma](https://bryanmed.github.io/correccionGamma/), de hecho, es posible utilizar funciones de mapeo que son definidas de manera arbitraria por el usuario.

Como su nombre indica, las transformaciones lineales por partes buscan crear una función de mapeo que se adapte a las necesidades del usuario mediante aproximanciones de rectas. Entre estas técnicas, una de las más populares es el llamado _contrast stretching_ ("estiramiento de contraste") que como su nombre indica, tiene como objetivo expandir el rango de intensidades de la imagen.

El primer paso de esta metodología es visualizar el [histograma](https://bryanmed.github.io/histograma/) de la imagen, el cual nos ayudará a identificar el __rango dinámico__. Con esto, en caso de contar con una distribución de valores muy estrecha, la diferencia de intensidades entre pixeles será muy pequeña, percibiéndose así como una ilustración en donde es difícil diferenciar los elementos de esta. Tomemos como ejemplo la imagen de un abdomen adquirida por rayos X que se muestra en la __Figura 2.1__, en ella vemos que exhibe un muy bajo contraste, lo cual es confirmado por el histograma correspondiente, en donde observamos que el rango de valores que tiene la imagen está concentrado en el rango de 80 a 175. 

{: .center}
![linearF]({{ site.baseurl }}/images/linearF.PNG)
__Figura 2.1__ _lalalaalala_.

A continuación, es definida la función de mapeo tomando en consideración el rango de valores de la imagen anterior, que serán proyectados a un rango más grande. La recta en verde (__Figura 2.2__) será la encargada de mapear las intensidades de entrada (80 - 175 en el eje X) a los niveles de brillo en la salida (0 - 255 en el eje Y).

{: .center}
![linearM]({{ site.baseurl }}/images/linearMapping.PNG)
__Figura 2.2__ _lalalaalala_.

Finalmente en la __Figura 2.3__ observamos el resultado de esta operación, que como podemos notar, obtenemos una imagen con un mayor contraste, en donde es posible identificar con mayor claridad detalles. En el histograma podemos constatar que las intensidades de esta nueva imagen ocupan todo el rango de valores disponibles en una imagen tipo Uint8 (256 niveles de brillo), y que, como hablaremos más adelante en el tema de [histogram matching](www.bryanmed.github.io), permite obtener imágenes más nítidas.

{: .center}
![linearG]({{ site.baseurl }}/images/linearG.PNG)
__Figura 2.3__ _lalalaalala_.

En la __Figura 2.4__ se muestra otro ejemplo, con una imagen viejita de la iglesia de Santa Catarina, en Rioverde, SLP.

{: .center}
![linearG]({{ site.baseurl }}/images/rioverde.PNG)
__Figura 2.4__ _lalalaalala_.


https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728
https://homepages.inf.ed.ac.uk/rbf/HIPR2/stretch.htm
http://siglo.inafed.gob.mx/enciclopedia/EMM24sanluispotosi/municipios/24024a.html
https://www.quia.com/pages/ra110a.html
