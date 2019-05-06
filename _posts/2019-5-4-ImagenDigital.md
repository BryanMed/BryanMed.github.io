---
layout: post
comments: true
mathjax: true
title: Introducción al Procesamiento Digital de Imágenes
---

## Imagen Digital

La adquisición de las imágenes se da a partir de un arreglo de sensores, encargados de transformar un fenómeno (físico o químico) a una variable eléctrica, esta señal es posteriormente digitalizada, es decir, _cuantificada_ a valores discretos, los cuales corresponden a los niveles de intensidad con los que será formada la imagen de salida. Un ejemplo de este proceso (mostrado en la __Figura 1.2__) es la obtención de una fotografía digital, en donde la luz reflejada por la escena a capturar incide sobre un conjunto de lentes cuya labor es el de enfocar la luz hacia una matriz de filtros, encargados de separar el espectro de la luz en las longitudes de onda correspondientes a los colores Rojo, Verde y Azul. Posteriormente, esta luz llegará a una malla de millones de sensores fotoeléctricos, que se encargarán de transformar la iluminación en un voltaje cuyos valores serán proporcionales a la cantidad de luz que inciden sobre ellos. Finalmente, la señal eléctrica será discretizada y almacenada para su posterior visualización.

{: .center}
![imagendigital]({{ site.baseurl }}/images/digitalImage.PNG)
 __Figura 1.2__ _Diagrama muy simplificado de la obtención de una fotografía digital_.

Antes de continuar con esta explicación, es importante resaltar que una imagen es una manera de representar la información, y no necesariamente muestra una escena que también sea observable por el ojo humano (como el caso anterior). De hecho, es tanta la variedad de sensores que permiten adquirir información dentro de casi todo el espectro electromagnético, que se abre un abanico muy grande de posibilidades, desde observar objetos muy lejanos (galaxias a partir de las ondas gamma), observar dentro de tejidos, sin dañarlos (rayos X), observar la temperatura de objetos (infrarrojos), entre muchas otras aplicaciones más, como se ejemplifica en la __Figura 1.3__.



Ahora bien, una imagen digital es una función bidimensional $$f(x, y)$$, en donde $$f$$ se refiere al nivel de intensidad (brillo) que se encuentra en determinada posición $$(x, y)$$. Estas imágenes son representadas como una matriz de tamaño $$M \times N$$, de la forma:

$$
f(x, y) = \begin{bmatrix}
f(0,0) & f(0,1) & ... & f(0, N-1)\\ 
f(1,0) & f(1,1) & ... & f(1, N-1)\\ 
... & ... &  & ... \\ 
f(M-1, 0) & f(M-1, 1) & ... & f(M-1, N-1)
\end{bmatrix}
$$

En donde cada elemento de este arreglo es conocido como __pixel__ (del inglés _picture element_), y es la unidad mínima
por la cual está conformada una imagen (__Figura 1.4__).




En el caso de las _imágenes a color_ cada pixel almacena 3 valores correspondientes a la intensidad de los canales Rojo, Verde y Azul. Por simplicidad, a lo largo del blog estaremos trabajando con imágenes en _escala de grises_ en donde por cada posición, solo encontraremos un valor de intensidad. 

en la __Figura 1.3__ observamos como la combinación de los 3 canales resulta en la imagen a color. No obstante, a lo largo del blog trabajaremos con _imágenes en escala de grises_ debido a que los algoritmos que veremos son extensibles al color los métodos en cada canal.











## Procesamiento Digital de Imágenes
Es un conjunto de técnicas que tiene como finalidad obtener una representación más adecuada de la imagen, además, es también utilizado en la extracción de características relevantes de esta, las cuales muchas veces no son perceptibles a primera vista. En la __Figura 1.1__ se observan ambos enfoques.

{: .center}
![imageprocessing]({{ site.baseurl }}/images/imageprocessing1.png)
 __Figura 1.1__ _La mejora de la imagen (image enhancement) y la extracción de características (feature extraction) son los dos principales objetivos que plantea el procesamiento digital de imágenes._

Antes de continuar con los métodos que se utilizan, es necesario definir una __imagen digital__.

