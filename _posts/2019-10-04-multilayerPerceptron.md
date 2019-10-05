---
layout: post
comments: true
mathjax: true
title: IA-2 > Redes neuronales - Perceptrón multicapa
---

¡Han pasado 84 años!... Anteriormente observamos que el perceptrón es capaz de emular el comportamiento de una compuerta lógica OR o AND al poder diferenciar los estados de encendido(1) o apagado(0) de acuerdo a las entradas que reciba. En la __Figura 1__ podemos observar las rectas que generan los perceptrones para separar las distintas clases.



Ahora, ¿qué pasaría si intentaramos que un perceptrón actúe como una compuerta XOR? recordando que esta compuerta genera una salida verdadera cuando los estados de sus dos entradas son diferentes entre sí, y una salida falsa cuando son iguales, como vemos en la __Figura 2__ en donde también podemos observar la manera en la que se distribuyen los estados de acuerdo a sus entradas.



Así que sería el momento de entrenar al perceptrón, pero pronto caeremos en la triste realidad de que nunca va a converger, ya que es imposible hacer que una línea recta (generada por el perceptrón) sea capaz de separar adecuadamente estos puntos __Figura 3__.




De hecho, la principal limitación del perceptrón es que permite resolver solo problemas _linealmente separables_ (aquellos donde podemos dividir un plano en 2 regiones mediante una línea recta). En cambio, con los problemas linealmente no separables el pequeño perceptrín chafea :/ __Figura 4__




Pero bueno, volviendo al caso de la puerta XOR podemos pensar que si usamos dos neuronas podremos generar dos líneas que me dividan el plano en 3 regiones __Figura 5__ funciona (kinda) pero no es necesariamente la solución que estamos buscando, pero, si nos ayuda a desarrollar la intuición de que ¡la unión hace la fuerza!. Así que nos daremos a la tarea de hacer que los perceptrones trabajen en conjunto, dando origen a las (taráááán) __R E D E S__ $$\;$$ __N E U R O N A L E S__.




## Estructura de una Red Neuronal
Hay distintos tipos de redes neuronales, una de las más populares es el _Perceptrón multicapa_. La parte de _Perceptrón_ ya la conocemos, y de _multi_ podemos inferir que se refiere a _varias_, así que, ¿de qué van las capas?... para ello veamos la __Figura 6__ en la cual mostramos una estructura de una Multilayer perceptron, pues bien, las capas son aquellas alineaciones verticales de las neuronas.



Podemos encontrar 3 tipos de capas:
* Capa de entrada: Conformadas por las neuronas en las cuales se ingresan los valores de mmm entrada je, por ello, contaremos con tantas neuronas como variables de entrada tengamos. En estas neuronas no se realiza procesamiento.

* Capa de Salida: Constituida por las neuronas que arrojarán la preddición de la red.

* Capas ocultas: Son las que se encuentran entre las capas de salida y las de entrada.



Organizamos la red por capas, y observamos que cada neurona está conectada con todas las neuronas de la capa anterior y posterior, con esto estamos realizando un proceso jerárquico, en donde las primeras capas se encargarán de identificar características simples, y conforme avancemos en capas, así lo hará la complejidad del conocimiento.



Pero no tan rápido, si trabajamos con el perceptrón como lo conocemos (o a lo que he explicado) la red neuronal será aún incapaz de resolver problemas linealmente no separables, y esto es debido a la función de activación de la neurona.

## Funciones de activación

Las funciones de activación nos indican la respuesta que genera el perceptrón a partir de sus entradas. Recordando, la respuesta de una neurona se genera mediante:

$$z = (\sum_{i} x_i \cdot w_i) - \theta$$

En donde $$x_{i}$$ son los valores de entrada, $$w_{i}$$ los pesos correspondientes y $$\theta$$ el umbral de disparo (bias). Ahora, para determinar si la neurona se dispara o no, condicionamos que si $$z$$ es mayor a 0 el perceptrón se activa:

$$
a = \left\{
    \begin{array}{ll}
        0 & \mbox{si } z < 0 \\
        1 & \mbox{si } z \geq 0
    \end{array}
\right.
$$

Precisamente la condición anterior es nuestra función de activación, mejor conocido como _función de paso unitario_ __Figura 7__, sin embargo, esta función tiene la principal desventaja de que no es diferenciable (en 0 está indeterminada) y dado que los algoritmos de aprendizaje (como el backpropagation que veremos más adelante) requieren de funciones de activación diferenciables, evita que sea una buena opción. El hecho de que el principal objetivo sea obtener unos pesos $$w$$ y bias $$b$$ que aproximen de buena manera la salida esperada, hacen de esto un proceso de optimización, en donde deseamos que las pequeñas variaciones de $$w$$ y $$b$$ produzcan pequeñas variaciones en la salida, pero al poder generar solo 2 valores (0 y 1) hace improbable esta optimización. Es entonces cuando entran en juego otras funciones de activación. 

## Función de activación Sigmoide
La función sigmoide __Figura 8__ está determinada por:

$$\frac{1}{1 + e^{-x}}$$

Esta función nos permite obtener a la salida valores que están acotados entre 0 - 1, es decir, una función de probabilidad.




## Función de activación ReLU
Siendo de las más utilizadas, la función Unidad Rectificada Lineal __Figura 9__ que está modelada por:

$$
ReLU = \left\{
    \begin{array}{ll}
        0 & \mbox{si } z < 0 \\
        x & \mbox{si } z \geq 0
    \end{array}
\right.
$$

Se dice que es la que mejor emula el comportamiento de las neuronas biológicas, además de que permite al modelo aprender más rápido y con y en la gran mayoría de casos con un mejor performance.






Existen muchísimas más [funciones de activación](https://en.wikipedia.org/wiki/Activation_function), pero por ahora trabajaremos con estas.





















