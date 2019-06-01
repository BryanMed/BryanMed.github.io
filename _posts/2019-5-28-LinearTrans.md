---
layout: post
comments: true
mathjax: true
title: 2.4| Transformacion lineal por partes (contrast stretching)
---

Las transformaciones que modifican los niveles de intensidad de una imagen no tienen porqué estar limitados a funciones matemáticas bien definidas, como la [Transformación logaritmo](https://bryanmed.github.io/TransformacionLogaritmo/) o [Transformación gamma](https://bryanmed.github.io/correccionGamma/), de hecho, es posible utilizar funciones de mapeo que son definidas de manera arbitraria por el usuario.

Como su nombre indica, las transformaciones lineales por partes buscan crear una función de mapeo que se adapte a las necesidades del usuario mediante aproximanciones de rectas. Entre estas técnicas, una de las más populares es el llamado _contrast stretching_ ("estiramiento de contraste") que como su nombre indica, tiene como objetivo expandir el rango de intensidades de la imagen. 

En este ejemplo crearemos la función de mapeo a partir de 3 rectas ...

