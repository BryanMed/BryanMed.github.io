---
layout: post
comments: true
mathjax: true
title: Introducción al Procesamiento Digital de Imágenes
---

## Procesamiento Digital de Imágenes
Es un conjunto de técnicas que tiene como finalidad obtener una representación más adecuada de la imagen, además, es también utilizado en la extracción de características relevantes de esta, las cuales muchas veces no son perceptibles a primera vista. En la __Figura 1.1__ se observan ambos enfoques.

{: .center}
![imageprocessing]({{ site.baseurl }}/images/imageprocessing1.png)
 __Figura 1.1__ _La mejora de la imagen (image enhancement) y la extracción de características (feature extraction) son los dos principales objetivos que plantea el procesamiento digital de imágenes._

Antes de continuar con los métodos que se utilizan, es necesario definir una __imagen digital__.

## Imagen Digital
La adquisición de las imágenes se da a partir de un arreglo de sensores, los cuales se encargan de transformar un fenómeno (físico o químico) a una variable eléctrica, esta señal es posteriormente digitalizada, es decir, _cuantificada_ a valores discretos, los cuales corresponden a los niveles de intensidad con los cuales será formada la imagen de salida. Un ejemplo de este proceso (mostrado en la __Figura 1.2__) es la obtención de una fotografía digital, en donde la luz reflejada por la escena a capturar incide sobre un conjunto de lentes cuya labor es el de enfocar la luz hacia una matriz de filtros, encargada de separar el espectro de la luz en las longitudes de onda correspondientes a los colores Rojo, Verde y Azul. Posteriormente, esta luz llegará a una malla de millones de sensores fotoeléctricos, los cuales se encargan de transformar la iluminación en un voltaje cuyos valores serán proporcionales a la cantidad de luz que inciden sobre ellos. Finalmente, la señal eléctrica será discretizada y almacenada para su posterior visualización.




Solemos asociar 
