---
layout: post
comments: true
mathjax: true
title: 4.2| Detección de Bordes - Derivadas
--- 

Como mencionamos brevemente en el [post de convolución](https://bryanmed.github.io/kernelsConv/), la diferenciación junto con la convolución son las herramientas predilectas en cuanto a la detección de bordes se refiere.

El detector de bordes debe de contar con las propiedades que se enlistan a continuación, además mencionamos como las derivadas fungen de buena manera estas funciones.

* Primero, en las zonas de brillo uniforme (donde no existen cambios de intensidad), nuestro detector nos debe indicar: "pues aquí no hay bordes, men, todo tranqui". Y bueno, precisamente el resultado de derivar una constante es 0 ($$f(c) = 0$$), así que punto para las derivadas.

* Segundo, en las zonas donde existe una transición de intensidad (yup, bordes) debería existir una respuesta por parte de nuestro detector tipo: "may, aquí hay algo". Y la diferenciación aparece de nuevo para ayudarnos con esta tarea, ya que la derivada de una _variación x_ es 1 ($$f(x) = 1$$).

