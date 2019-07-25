---
layout: post
comments: true
mathjax: true
title: 4.2| Detección de Bordes - Derivadas
--- 
Como mencionamos en la clasificación de bordes, la función rampa es la más común de encontrar en una imagen debido a que las transiciones de intensidad no son tan abruptas (como lo sería una función escalón), esto en parte porque en la práctica los bordes de una imagen regularmente se encuentran un tanto borrosos, por factores como las limitaciones del mecanismo de enfoque, o ruido agregado por los componentes eléctricos del sistema de adquisición, entre otros. Es por ello que trabajaremos con el modelo de rampa para explicar la detección de bordes. 

Y bueno, para detectar bordes la herramienta predilecta es _la[convolución](https://bryanmed.github.io/kernelsConv/)_, en donde haremos pasar un kernel que debe contar con las siguientes características:

1. En las zonas de brillo uniforme (donde no existen cambios de intensidad a.k.a)


, nuestro detector nos debe indicar: "pues aquí no hay bordes, men, todo tranqui". Y bueno, precisamente el resultado de derivar una constante es 0 ($$f(c) = 0$$), así que punto para las derivadas.

2. En las zonas donde existe una transición de intensidad (yup, bordes) debería existir una respuesta por parte de nuestro detector tipo: "may, aquí hay algo". Y la diferenciación aparece de nuevo para ayudarnos con esta tarea, ya que la derivada de una _variación x_ es 1 ($$f(x) = 1$$).

