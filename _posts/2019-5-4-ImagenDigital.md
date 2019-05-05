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
La adquisición de las imágenes se da a partir de un arreglo de sensores, los cuales son encargados de transformar un fenómeno (físico o químico) a una variable eléctrica, finalmente esta señal es digitalizada, es decir, _cuantificada_ a valores discretos, los cuales corresponderán a niveles de intensidad en la imagen que sea construida. El ejemplo clásico es el de una fotografía digital, en donde se utilizan sensores fotoeléctricos (conversión luz &rarr electricidad)
