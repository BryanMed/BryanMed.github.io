---
layout: post
comments: true
mathjax: true
title: 4.2| Detección de Bordes - Derivadas
--- 
Como mencionamos en la clasificación de bordes, la función rampa es la más común de encontrar en una imagen debido a que las transiciones de intensidad no son tan abruptas (como lo sería una función escalón), esto en parte porque en la práctica los bordes de una imagen regularmente se encuentran un tanto borrosos, por factores como las limitaciones del mecanismo de enfoque, o ruido agregado por los componentes eléctricos del sistema de adquisición, entre otros. Es por ello que trabajaremos con el modelo de rampa para explicar la detección de bordes. 

Y bueno, para detectar bordes la herramienta predilecta es _la [convolución](https://bryanmed.github.io/kernelsConv/)_, en donde básicamente hacemos pasar un kernel por toda la imagen, y por cada pixel de esta obtendremos una respuesta que es dependiente tanto de los valores del kernel, así como de la vecindad del pixel correspondiente.

Bien, entonces ya sabemos que un borde es una transición de intensidad en un tiempo relativamente corto de tiempo, y que para detectarlos usamos la convolución, pero, ¿qué características buscamos en un _edge detector_?... principalmente dos: 

1. Que en las zonas de brillo uniforme (donde no existen cambios tan grandes de intensidad) la respuesta del detector sea mínima. "Pues aquí no hay nada men, todo tranqui".

2. Por otro lado, en la zonas donde existe un cambio "abrupto" de intensidad, la respuesta del detector debe ser grande (y por respuesta me refiero al valor resultante de la convolución), que nos indique "épale men, here´s something".


, nuestro detector nos debe indicar: "pues aquí no hay bordes, men, todo tranqui". Y bueno, precisamente el resultado de derivar una constante es 0 ($$f(c) = 0$$), así que punto para las derivadas.

2. En las zonas donde existe una transición de intensidad (yup, bordes) debería existir una respuesta por parte de nuestro detector tipo: "may, aquí hay algo". Y la diferenciación aparece de nuevo para ayudarnos con esta tarea, ya que la derivada de una _variación x_ es 1 ($$f(x) = 1$$).

