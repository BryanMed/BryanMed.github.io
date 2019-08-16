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
La explicación que daré de la neurona es muy pero muy superficial, pero servirá para comprender el concepto,  en la __Figura 1__ observamos un dibujo de una neurona, la cual a grandísimos rasgos, se encuentra conformada por:

*	Soma o cuerpo de la neurona, en donde encontramos el nucleo celular.
*	Dendritas, las cuales son prolongaciones que salen del soma y son las encargadas de recibir la información y conducirla hacia el soma.
*	Axón, es el encargado de trasmitir la información desde el cuerpo celular hacia la periferia.

{: .center}
![zorroOscuro]({{ site.baseurl }}/images/zorroOscuro.PNG)
__Figura 1__ _observamos la pobre distribución de los niveles de intensidad utilizados en la imagen, los cuales se encuentran en los niveles bajos, lo que resulta en una imagen oscura de poco contraste_.
 
Cada neurona cuenta con solo un axón, el cual se ramifica en su porción terminal, lo que permitirá comunicarse con otras dendritas en el proceso de sinapsis. El proceso por el que una neurona puede generar un potencial de acción (señal de salida) se realiza (a grandes rasgos) de la siguiente manera: La célula recibe estímulos internos a partir de las dendritas, y sumaremos las intensidades de estas señales. Para general el potencial de acción, se sigue la ley de “todo o nada” en la que la neurona cuenta con un umbral de excitación. En donde, si el estímulo es mayor al umbral, se genera el potencial de acción, y en caso de no superarlo pues no. Lo interesante acá, es que no importa la intensidad de la señal que forman los estimulos, siempre que se supere el umbral, se generará el mismo potencial de acción.

### El Perceptrón
Y tomando en cuenta el comportamiento anterior, es como se creó el modelo del perceptrón (el cual es muy similar al comportamiento de un transistor). Al perceptrón llegarán señales de entrada (el análogo a las dendritas) $$x_n$$, y generará una salida (el paralelismo al axón). Cada entrada podrá recibir únicamente valores binarios (0 o 1), cuya importancia será ponderada de acuerdo a un peso $$w$$. Finalmente la salida $$z$$ (equivalente al potencial de acción) dependerá de:

*	El valor que tomen las entradas $$x_n$$
*	De sus pesos $$w_n$$
*	Un umbral de disparo de la neurona o _bias_ ($$\theta$$)
 
Es así que la salida $$z$$ se genera a partir de la siguiente función:

$$z = (\sum_{i} x_i \cdot w_i) - \theta$$

Por comodidad, restamos de una vez el umbral $$\theta$$. Así, si esta señal $$z$$ es mayor o igual a cero, el perceptrón se dispara (salida $$z$$ = 1), en caso de no alcanzar el umbral, la salida será 0.

$$
z = \left\{
    \begin{array}{ll}
        0 & \mbox{si } z > 0 \\
        1 & \mbox{si } z \geq 0
    \end{array}
\right.
$$

Es ahora que entra en juego un proceso de _entrenamiento_ (así es, en este caso en particular estamos hablando de un _aprendizaje supervisado_) en donde a la red se le dan ejemplos de los resultados esperados, a fin de que sea capaz de generar una respuesta, la cual si llega a ser muy distinta del valor deseado, se tendrán que ajustar los parámetros.

Pero mejor veamos un ejemplo de juguete, supongamos que quiero que un perceptrón me ayude a encontrar el amorts, para escoger a mi chica ideal tomaré en cuenta solo dos factores:

*	$$x_1$$ = Que tenga buenos sentimientos.
*	$$x_2$$ = Que esté bonita.

Una vez entrenado,  el perceptroncito arroja los siguientes valores: 

* $$w_1$$ = 0.5
* $$w_2$$ = -0.4
* $$\theta$$ = 0.3

Si estos datos los pasamos a la fórmula para conocer $$z$$, nos daremos cuenta que es la ecuación de una recta (z = $$0.5x_1 - 0.4x_2 + 0.3$$), en la __Figura #__ observamos que esta línea crea un _sesga_ a mis prospectos, en donde aquellas chicas que quedan debajo de la recta son muy probables a lastimar mi corazón :(, por otro lado, las que están por encima de esta barrera, ¡si a todo!.

{: .center}
![zorroOscuro]({{ site.baseurl }}/images/zorroOscuro.PNG)
__Figura 1__ _observamos la pobre distribución de los niveles de intensidad utilizados en la imagen, los cuales se encuentran en los niveles bajos, lo que resulta en una imagen oscura de poco contraste_.

Existe además otro elemento, llamado _factor de aprendizaje_ $$\lambda$$ el cual señala la velocidad de aprendizaje de la red. Un valor de aprendizaje alto, hará que nos quedemos a medias con la búsqueda de los valores ideales, por otro lado, un valor muy bajo hará que el tiempo de búsqueda sea poco eficiente, en donde los coeficientes estarán oscilando entre valores muy cercanos entre sí (redundante). Un valor usualón es de 0.2.

Oye Bryan y ¿cómo sabemos cuándo cambiar o no los parámetros? Ah, pues para ello utilizaremos el error $$e$$, es decir la diferencia entre nuestro valor de salida deseado $$y$$ y nuestro valor de salida actual:

$$ e =  (y – z) $$

Si el error es menor a un umbral (digamos < 0.1%), entonces nuestra estará lista. En caso contrario habrá que iterar hasta dar con esos valores. 

Y ahora te estarás preguntando en base a que o como ajustar los parámetros. En el caso del umbral $$\theta$$, se le suma este $$\Delta \theta$$:

$$ \Delta \theta = -(\lambda \cdot e)$$

Por otro lado, los pesos $$w$$ se ajustan al sumarle a cada uno el $$\Delta w$$ correspondiente:

$$\Delta w_{i} = \lambda \cdot e \cdot x_{i}$$

En general, el proceso de aprendizaje de un perceptrón consta de lo siguiente:

* Inicializar con variables aleatorios (pequeños) el bias $$\theta$$ y los pesos $$w_1$$ y $$w_2$$.
* Calcular la salida $$z$ de la red, de acuerdo a las entradas $$x_1, ... x_2$$.
* Calcular el error $$e$$ el cual es la diferencia entre el valor deseado $$y$$ y el valor obtenido $$z$$.
* Si el error es mayor a un 0.1%, entonces debemos de modificar los parámetros.
* Modificar el umbral $$\theta$$ y los pesos $$w_1$$ y $$w_2$$ según el error obtenido. 
* Repetir el proceso hasta que el error se encuentre en un rango aceptable, a lo largo de toda una iteración.
____
Ahora nos pondremos más guapos y vamos a entrenar un perceptrón desde 0, a mano. Nuestro objetivo es que el perceptrón funcione como una compuerta lógica AND. El comportamiento del operador está dado por la tabla de verdad que se muestra a continuación:
 
|  x  |  y  |x and y |
|:---:|:---:|:------:|
|  0  |   0 |    0   |
|  0  |   1 |    0   |
|  1  |   0 |    0   |
|  1  |   1 |    1   |
 
El primer paso es escoger los parámetros (peso y bias) de manera aleatoria (en toda la documentación que he encontrado sugieren utilizar valores pequeños), además, el factor de aprendizaje $$\lambda$$ regularmente se pone como 0.2, así:

* $$\lambda = 0.2$$
* $$\theta = 0.3$$
* $$w_1 = 0.4$$
* $$w_2 = 0.5$$

Ahora que tenemos nuestros ingredientes, vamos a realizar la primera iteración. Empezamos con el primer caso de la tabla de verdad, en aquel donde $$x_1 = 0$$ y $$x_2 = 0$$, cuyo valor de salida esperado es $$y = 0$$. Así, calculamos nuestra salida $$z$$:

$$z = (x_1 \cdot w_1) + (x_2 \cdot w_2) - \theta$$

$$z = (0 \cdot 0.4) + (0 \cdot 0.5) – 0.3 = -0.3$$

Como $$z < 0$$ entonces el perceptrón no se dispara, es decir, $$z = 0$$. Ahora verificamos el error:

$$e = y \quad – z$$

$$e = 0 \quad – 0 = 0

Como no hay error, pasamos al siguiente par de valores, $$x_1 = 0$$ y $$x_2 = 1$$ y cuyo valor esperado es $$y = 0$$. Repetimos el procedimiento anterior:

$$z = (0 \cdot 0.4) + (1 \cdot 0.5) – 0.3 = 0.2$$

Al ser $$z \geq 0$$ perceptrín se dispara, con lo cual la salida es $$z = 1$$. Al momento de comprobar el error tenemos:

$$e = 0 \quad – 1 = -1$$

Y Houston, tenemos un problema, el tener esta diferencia con el valor esperado nos indica que debemos de recalcular parámetros, para ello calcularemos sus factores de cambio, empezando por $$\Delta \theta$$:

$$\Delta \theta = -(\lambda \cdot \e)$$

$$\Delta \theta = -(0.2 \cdot -1) = 0.2$$

Y ahora a calcular los cambios de pesos:

$$\Delta w_i = \lambda \cdot e \cdot x_i$$

$$\Delta w_1 = 0.2 \cdot -1 \cdot 0 = 0$$

$$ \Delta w_2 = 0.2 \cdot -1 \cdot 1 = -0.2$$

Ahora sí, actualizamos los pesos y el bias:

* $$\theta = \theta + \Delta \theta$$

$$\theta = 0.3 + 0.2 = 0.5$$

* $$w_i = w_i + \Delta w_i$$

$$w_1 = 0.4 + 0 = 0.4$$

$$w_2 = 0.5 – 0.2 = 0.3$$

Atención aquí, estos parámetros que acabamos de recalcular son los que utilizaremos para calcular la salida en lo queda de esta iteración (a menos que tengamos que recalcular nuevamente estos valores), no esperamos a que acabe esta primera iteración. Continuando con el ejemplo, tenemos que las entradas siguientes son $$x_1 = 1$$ y $$x_2  = 0$$, con un valor esperado $$ y = 0$$, con lo cual:

$$z = (1 \cdot 0.4) + (0 \cdot 0.3) – 0.5 = -0.1$$

Como $$z < 0$$ el perceptrón no se dispara, por lo tanto $$z = 0$$. Al calcular el error:

$$e = 0 \quad – 0$$

Vemos que todo funciona smooth, por lo cual no actualizamos lo valores y pasamos a los siguientes valores. Teniendo finalmente el último caso de esta primera iteración $$x_1 = 1$$ y $$x_2 = 1$$ y un valor esperado $$y = 1$$:

$$z = (1 \cdot 0.4) + (1 \cdot 0.3) – 0.5 = 0.2$$

Como $$z \geq 0$$ el perceptrón se dispara, resultando en $$z = 1$$, al calcular el error vemos que

$$e = 1 – 1 = 0$$

No hay error, así que nos quedamos (por ahora) con estos valores.

Pero no tan rápido, aún no terminamos. El proceso de entrenamiento termina cuando logramos tener una iteración sin ningún error, así que es tiempo de pasar a la iteración 2, para no hacerla mucho de emoción, resumiré los resultado en la __Tabla 2__
X_1	X_2	Y	Z 	e
0	0	0	0	0
0	1	0	0	0
1	0	0	0	0
1	1	1	1	0


|  $$x_1$$  | $$x_2$$ | $$y$$ | $$z$$ | $$e$$ |
|:---------:|:-------:|:-----:|:-----:|:-----:| 
|     0     |    0    |   0   |   0   |   0   |
|     0     |    1    |   0   |   0   |   0   |
|     1     |    0    |   0   |   0   |   0   |
|     1     |    1    |   1   |   1   |   0   |

Como tenemos una iteración sin errores, hemos encontrado los pesos y el umbral correctos para que nuestro perceptrón se comporte de la manera que deseamos. En la __Figura #__ observamos como la recta resultante separa correctamente ambas clases.




