---
layout: post
comments: true
mathjax: true
title: 4.1| Detección de Bordes
--- 
Los _bordes (edges)_  son identificados como el límite que separa dos regiones dentro de una imagen. Entre las distintas características que existen para detectar los bordes, en este post trataremos unicamente los referentes a la variación de intensidad.

Y bueno, como mencionamos en el párrafo anterior, los bordes se forman a partir de _cambios abruptos_ (otros no tanto) del nivel de brillo, estos se clasifican de acuerdo a su perfil de intensidad de la siguiente manera:

* __Step edges__: Se encuentran en zonas donde existe un cambio súbito de intensidad (idealmente de un pixel a otro). Con lo cual estos bordes son modelados como una funcion de escalón unitario. Este es el borde ideal, sin embargo es poco usual encontrarlo en imágenes no artificales.
* __Ramp edges__: Estos se producen cuando el cambio de brillo no es instantáneo, si no que existe una ventana de tiempo en la que va variando hasta alcanzar la nueva intensidad. La función que la representa es precisamente la función rampa. Son de los más comunes de encontrar, dado que en la gran mayoría de imágenes encontramos ya sea ruido, o desenfoques que producen cierto suavizado en regiones, lo cual produce una transición más _smooth_ entre las regiones, resultando en una transición más lenta (asemejandose a la función rampa).
* __Roof edges__: 

Es así, que se pueden caracterizar como _cambios abruptos_ (y algunos no tanto) de intensidad. 

El objetivo de la detección de bordes es el de reducir en gran medida la cantidad de datos, al preservar únicamente la información concerniente a lo que delimita las estructuras.

