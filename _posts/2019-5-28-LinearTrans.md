---
layout: post
comments: true
mathjax: true
title: 2.4| Transformacion lineal por partes (contrast stretching)
---

Las transformaciones que modifican los niveles de intensidad de una imagen no tienen porqué estar limitados a funciones matemáticas bien definidas, como la [Transformación logaritmo](https://bryanmed.github.io/TransformacionLogaritmo/) o [Transformación gamma](https://bryanmed.github.io/correccionGamma/), de hecho, es posible utilizar funciones de mapeo que son definidas de manera arbitraria por el usuario.

Como su nombre indica, las transformaciones lineales por partes buscan crear una función de mapeo que se adapte a las necesidades del usuario mediante aproximanciones de rectas. Entre estas técnicas, una de las más populares es el llamado _contrast stretching_ ("estiramiento de contraste") que como su nombre indica, tiene como objetivo expandir el rango de intensidades de la imagen.

El primer paso de esta metodología es visualizar el [histograma](https://bryanmed.github.io/histograma/) de la imagen, el cual nos ayudará a identificar el __rango dinámico__, que indica la variedad de intensidades que presenta una imagen, así, entre mayor sea este rango, mayor será la cantidad de valores disponibles en la representación y por ende mostrará un mayor contraste. Tomemos como ejemplo la imagen con bajo contraste mostrada en la __Figura 2.1__ en la cual notamos que es dificil de distinguir detalles, a la derecha encontramos el histograma correspondiente, en donde notamos el pequeño rango en el cual se encuentra, lo que produce que la 


