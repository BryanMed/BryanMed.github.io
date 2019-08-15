---
layout: post
comments: true
mathjax: true
title: IA-1 > Redes neuronales - El Perceptrón.
---
En esta nueva serie de posts, hablaremos acerca de la _inteligencia artificial_. En esta ocasión saltaré directamente a las redes neuronales dado que serán necesarias para proyectos futuros, sin más, vamos a ello.

El ser humano siempre ha tomado como referencia a la naturaleza para desarrollar herramientas cada vez más eficientes. Ejemplos hay muchos, como la manera en la que la morfología de las aves inspira al diseño de aviones, permitiendo mejorar diversos aspectos como resistencia al viento, consumo de combustible, etc. En la arquitectura, donde se nota la manera en la que se utilizan las estructuras de las plantas para lograr un diseño estético y sobretodo funcional. 

Y bueno, un área que también hace uso de esto son las ciencias de la computación, donde el comportamiento de las manadas, funcionamiento de sistemas biológicos y la herencia de los genes (por mencionar algunos). Un libro que llamó mi atención a la programación es precisamente el [nature of code de Daniel Shiffman]( https://natureofcode.com/) en donde presenta algoritmos basados en fenómenos naturales, encaminados a creas efectos visuales. 

Pues bien, en cuanto a la inteligencia artificial, uno de los métodos más populares son las _redes neuronales_ que precisamente toma como inspiración el funcionamiento de la neurona biológica para crear un modelo capaz de solucionar problemas. 

### La neurona biológica
La explicación que daré de la neurona es muy pero muy superficial, pero servirá para comprender el concepto. A grandísimos rasgos, se encuentra conformada por:

*	Soma o cuerpo de la neurona, en donde encontramos el nucleo celular.
*	Dendritas, las cuales son prolongaciones que salen del soma y son las encargadas de recibir la información y conducirla hacia el soma.
*	Axón, es el encargado de trasmitir la información desde el cuerpo celular hacia la periferia
 
Cada neurona cuenta con solo un axón, el cual se ramifica en su porción terminal, lo que permitirá comunicarse con otras dendritas en el proceso de sinapsis. El proceso por el que una neurona puede generar un potencial de acción (señal de salida) se realiza (a grandes rasgos) de la siguiente manera: La célula recibe estímulos internos a partir de las dendritas, y sumaremos las intensidades de estas señales. Para general el potencial de acción, se sigue la ley de “todo o nada” en la que la neurona cuenta con un umbral de excitación. En donde, si el estímulo es mayor al umbral, se genera el potencial de acción, y en caso de no superarlo pues no. Lo interesante acá, es que no importa la intensidad de la señal que forman los estimulos, siempre que se supere el umbral, se generará el mismo potencial de acción.

### El Perceptrón
Y tomando en cuenta el comportamiento anterior, es como se creó el modelo del perceptrón (el cual es muy similar al comportamiento de un transistor). Al perceptrón llegarán señales de entrada (el análogo a las dendritas) $$x_n$$, y generará una salida (el paralelismo al axón). Cada entrada podrá recibir únicamente entradas binarias (0 o 1), cuya importancia será ponderada de acuerdo a un peso $$w$$. Finalmente la salida $$z$$ (equivalente al potencial de acción) dependerá de:

*	El valor que tomen las entradas $$x_n$$
*	De sus pesos $$w_n$$
*	Un umbral de disparo de la neurona ($$\theta$$)
 
Es así que la salida $$z$$ se genera a partir de la siguiente función:

$$z = (\sum_{i} x_i \cdot w_i)) - \theta$$

Por comodidad, restamos de una vez el umbral $$\theta$$. Así, si esta señal $$z$$ es mayor o igual a cero, el perceptrón se dispara (salida $$z$$ = 1), en caso de no alcanzar el umbral, la salida será 0.

Es ahora que entra en juego un proceso de _entrenamiento_ (así es, las redes neuronales son parte del aprendizaje supervisado) en donde a la red se le dan ejemplos de los resultados esperados, a fin de que sea capaz de generar una respuesta, la cual si llega a ser muy distinta del valor deseado, se tendrán que ajustar los parámetros.

Pero mejor veamos un ejemplo de juguete, supongamos que quiero que un perceptrón me ayude a encontrar el amorts, para escoger a mi chica ideal tomaré en cuenta solo dos factores:

*	$$x_1$$ = Que tenga buenos sentimientos.
*	$$x_2$$ = Que esté bonita.

Una vez entrenado,  el perceptroncito arroja los siguientes valores: 

* $$w_1$$ = 0.5
* $$w_2$$ = -0.4
* $$\theta$$ = 0.3

Si estos datos los pasamos a la fórmula para conocer $$z$$, nos daremos cuenta que es la ecuación de una recta y como vemos en la __Figura #__ esta línea crea un _sesga_ a mis prospectos, en donde aquellas chicas que quedan debajo de la recta son muy probables a lastimar mi corazón :(, por otro lado, las que están por encima de esta barrera, ¡si a todo!.





Existe además otro elemento, llamado _factor de aprendizaje_ $$\lambda$$ el cual señala la velocidad de aprendizaje de la red. Un valor de aprendizaje alto, hará que nos quedemos a medias con la búsqueda de los valores ideales, por otro lado, un valor muy bajo hará que el tiempo de búsqueda sea poco eficiente, en donde los coeficientes estarán oscilando entre valores muy cercanos entre sí (redundante). Un valor usualón es de 0.2.

Oye Bryan y ¿cómo sabemos cuándo cambiar o no los parámetros? Ah, pues para ello utilizaremos el error $$e$$, es decir la diferencia entre nuestro valor de salida deseado $$y$$ y nuestro valor de salida actual:

$$ e =  (y – z) $$

Si el error es menor a un umbral (digamos < 0.1%), entonces nuestra estará lista. En caso contrario habrá que iterar hasta dar con esos valores. 

Y ahora te estarás preguntando en base a que o como ajustar los parámetros. En el caso del umbral $$\theta$$, se le suma este $$\Delta \theta$$:

$$ \Delta \theta = -(\lambda \cdot e)$$

Por otro lado, los pesos $$w$$ se ajustan al sumarle a cada uno el $$\Delta w$$ correspondiente:

$$\Delta w_{i} = \lambda \cdot e \cdot x_{i}$$


| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |



