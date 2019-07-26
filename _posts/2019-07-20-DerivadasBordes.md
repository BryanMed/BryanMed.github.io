---
layout: post
comments: true
mathjax: true
title: 4.2| Detección de Bordes - Derivadas
--- 
En este post explicaremos el papel que juega la convolución y las derivadas en la detección de bordes. Para fines prácticos y de visualización, usaremos el modelo "ideal" de _impulso unitario_ el cual es el modelado de un borde muy "sharp" (transición de intensidad muy abrupta).

Y bueno, para detectar bordes la herramienta predilecta es _la [convolución](https://bryanmed.github.io/kernelsConv/)_, en donde básicamente hacemos pasar un kernel por toda la imagen, y por cada pixel de esta obtendremos una respuesta que es dependiente tanto de los valores del kernel, así como de la vecindad del pixel correspondiente.

Bien, entonces ya sabemos que un borde es una transición de intensidad en un tiempo relativamente corto de tiempo, y que para detectarlos usamos la convolución, pero, ¿qué características buscamos en un _edge detector_?... principalmente dos: 

* Que en las zonas de brillo uniforme (donde no existen cambios tan grandes de intensidad) la respuesta del detector sea mínima. "Pues aquí no hay nada men, todo tranqui".

* Por otro lado, en la zonas donde existe un cambio "abrupto" de intensidad, la respuesta del detector debe ser grande (y por respuesta me refiero al valor resultante de la convolución), que nos indique "épale men, here´s something".

Es ahora cuando viene la pregunta ¿Existirá algo que permita generar este tipo de respuestas tan específicas?. Aquí es cuando entran en juego las _derivadas_ que, long story short, son las _diferencias_ entre valores consecutivos, el qué tanto cambió el valor actual respecto al valor pasado. Tomemos como ejemplo la función rampa de la __Figura 1__.


La transición entre los valores se da en el "pixel" 5, en donde las intensidades de los "pixeles" anteriores a este son 0.0, en cambio, el brillo de los "pixeles" posteriores a este son 1.0, podemos observar que el borde se encuentra precisamente en este cambio de intensidad, en el punto 5. 

Ahora recomiendo mucho leer la sección de _operadores de sharpening_ del post de [convolución](https://bryanmed.github.io/kernelsConv/) ya que ahí explico un poquito el transfondo del kernel de derivada. Resumiendo un poquito, la derivada de una señal $$f$$ se puede aproximar como las diferencias de valores consecutivos, de la forma:

$$\frac{\partial f}{\partial x} = f(x + 1) - f(x)$$

Como podemos notar, al valor pasado $$f(x + 1)$$ (recuerda que en una señal el "x + 1" indica un retraso en la señal de 1 unidad) le estamos restando el valor actual $$f(x)$$, es por ello que podemos representar esta señal con el kernel de convolución siguiente:

$$w_{dv1} = [-1 \qquad 1]$$

una versión que permite que el resultado de la convolución esté centrado en el punto correspondiente, es:

$$w_{dv1} = [-1 \qquad 0 \qquad 1]$$



