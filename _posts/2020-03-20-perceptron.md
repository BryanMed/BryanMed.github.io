---
layout: post
comments: true
mathjax: true
title: ML-1| Percetrón
---

¡Hola! después de un tiempito, publicaré algunos posts enfocados en el Machine Learning, quiero agradecer al [Dr. Onofre Orozco](https://www.researchgate.net/profile/Onofre_Orozco) por su apoyo y explicaciones en estos temas. 

El objetivo de estos posts es hacerlos un poco más interactivos, es por ello que publicaré una versión del código en Google Colab (una jupyter notebook) para que puedas correr las implementaciones sin instalar nada en tu pc, solo necesitas contar con internet y tu cuenta de Gmail. 

# La Neurona biológica

La unidad principal del sistema nervioso central, y se encarga de **recibir**, **procesar** y **transmitir** información a través de señales electroquímicas. Estas características en su funcionamiento despertarón el interés para crear un modelo que emulara este comportamiento. En la siguiente imagen podemos observar un modelo de una neurona, en donde discutiremos la función de algunas de sus partes que más llaman nuestro interés.

![neurona](neurona.png)
> *neurona biológica, fotografía tomada de la [wiki](https://commons.wikimedia.org/wiki/File:Neurons_uni_bi_multi_pseudouni.svg)*

* **Dendritas:** Son las pequeñas ramificaciones que se encuentran en el soma, y su importancia recae en que su función principal es el recibir estimulos nerviosos provenientes de otras neuronas (sinápsis), y enviarlas al soma. Es importante considerar que no todos los impulsos de las neuronas que conectan con las dendritas tienen la misma intensidad, siendo determinado por distintos factores como la mielización de la neurona pre-sináptica (que tan bien se propaga la señal en el axón), cantidad de neurontransmisor, el número de conexiones del axón con las dendrítas, entre otros. 

* **Soma :** Es el cuerpo celular de la neurona, en donde se encuentra el citoplasma y otros orgánelos de gran importancia que se encargan de regir el funcionamiento y mantener con vida la unidad biológica. De entre las muchas funciones del soma, las que más nos interesan son: Que aquí se lleva a cabo la mayor parte de síntesis de las proteínas, en las que algunas son parte o promueven la creación de **neurontransmisores**. Es aquí donde se lleva a cabo el procesamiento de la información nerviosa y su reacción a ella.

* **Axón :** Es la gran prolongación/brazo que sale desde desde el soma, y es, de manera general, el encargado de la transmisión del impulso eléctrico, no obstante, para que se pueda generar este **Potencial de acción**, se tiene que superar un umbral de despolarización, el cual se logra en dos casos, 1) al llegar un estímulo lo suficientemente grande, o 2) la suma de varios estímulos dentro de un corto periodo de tiempo. Al superar este umbral, la neurona se "dispara" llegando la señal eléctrica al botón terminal, que será la señal de liberación de partículas químicas que llegarán a la neurona post-sináptica. _Transmitiendo una señal_.

# El Perceptrón 

Es básicamente una representación matemática muy burda del funcionamiento de la neurona biológica, que, en solitario, permite la resolución de problemas linealmente separables (más de esto más adelante, pero son aquellos problemas en los que podemos separar distintos grupos mediante lineas rectas). En el siguiente diagrama podemos observar una representación de este modelo y como trata de emular la estructura de la neurona. 

![perceptron](perceptron.PNG)
> *diagrama de un perceptrón/neurona matemática*

Ahora, vamos a discutir sus partes y paralelísmos con la neurona biológica

**Dendritas $[x]$:** Tenemos un vector $[x]$ como $n$ señales de entrada, que simulan los impulsos electroquímicos de neuronas externas.

$$ 
x = 
\begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{bmatrix}
$$

Estas señales serán multiplados por su correspondiente **peso sináptico** que se encargará de ponderar la intensidad de las señales de entrada. Los valores de este vector $w$ serán modificados de tal manera que permitan generar la salida deseada, en pocas palabras, los pesos $w$ son nuestra incognita.

$$ 
w = 
\begin{bmatrix}
w_1 \\
w_2 \\
\vdots \\
w_n
\end{bmatrix}
$$

Siguiendo el recorrido observamos que al llegar al soma, tenemos un conjunto de señales ponderadas, de la forma $x_n * w_n$, estas señales serán sumadas una vez se encuentren en el soma, es decir, sumaremos los productos de las señales de entradas con su respectivo peso sináptico, esta operación la conocemos como **producto punto** y la representamos de la siguiente manera:

$$z = w_1x_1 + w_2x2 + \dots + w_nx_n \\$$

$$z = [w_1, w_2, \dots, w_n] \begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{bmatrix} \\
$$

$$z = w^{T}\cdot x$$

En donde $z$ es la salida en esta etapa. Otro valor a considerar es el **bias** o umbral de activación de la neurona que está representado como el peso $w_0$, estos dos nombres ayudan a entender su funcionamiento, se le conoce como _umbral_ porque es el valor que tendrá que superar la sumatoria de señales ponderadas para activarse, es decir:

$$w^{T}\cdot x >= w_0$$

por comodidad pasamos este valor umbral al otro lado de la ecuación, de tal suerte que la neurona tendrá una activación excitatoria si supera el 0, e inhibitoria en el otro caso:

$$(w^{T}\cdot x) - w_0 >= 0$$

En el inglés, o al menos en twitter, la gente suele utilizar mucho este término para dar opiniones "biased" que se refiere a comentar de manera poco objetiva (basado en preferencias personales) por ejemplo, yo puedo decir que las hamburguesas de mi mamá son las mejores (que si es cierto) pero también podría decir eso por el hecho de que es mi familiar, es decir, llevo cierta preferencia por default. Pues lo mismo pasa con este término en las redes neuronales, es un término sobre el cual tenderá el valor de salida, vemos que la expresión $z = (w^{T}\cdot x) - w_0$ se asemeja mucho a la ecuación de la recta $y = mx + b$, pues bueno, la $b$ determina la intersección de la recta en el eje y actúa como un "offset" que permite ajustar la recta de mejor manera a aquellas funciones que no tienen una intersección por 0, y en el caso de las redes neuronales cuando no cuentan con un bias, será más difícil que la red aproxime ciertas funciones.

El siguiente paso es evaluar este impulso en una **función de activación $\phi$** que dictará el comportamiento de disparo de la neurona. Por ejemplo, la función de activación $\phi _{escalón}$ está definida de la siguiente forma:

$$
\phi _{escalón}(z) = \begin{cases}
1 & \mbox{if} \; z \geq \theta \\
0 & \mbox{if} \; z < \theta 
\end{cases}
$$

Al ver la gráfica de la función en la siguiente imagen, podemos observar el comportamiento de $\phi$, en donde para aquellos valores menos a 0, la función vale 0, y valdrá 1 en caso contrario. 

![step](step.png)
> *Función de activación de escalón unitario*

Finalmente podemos representar la señal de salida de la neurona mediante $\hat y$.

$$\hat y = \phi (w^{T}\cdot x - \theta) $$ 

Y pasaremos a la implementación de este algoritmo.

## Implementación del perceptrón 
Lo primero será importar las librerías necesarias para trabajar, en este caso la librería de métodos numéricos de python **Numpy** (**Num**erical **Py**thon) que nos permitirá operar con vectores y matrices (Está muy optimizada), y por otro lado, **Matplotlib** que usaremos para crear gráficas.

```python
import numpy as np
import matplotlib.pyplot as plt
```
El perceptrón lo escribí como una clase, pero podemos discutir algunas de sus funciones, por ejemplo su constructor

```python

def __init__(self, num_inputs, lr, epochs, pesos=None):
        if pesos:
            self.weights = pesos # en caso de contar con pesos del perceptron cargarlos
        else:
            self.weights = np.random.rand(num_inputs+1) # el peso extra es el bias
            
        self.lr = lr #learning rate
        self.epochs = epochs #num de iteraciones
```
Es decir que al momento de crear un objeto `perceptrón` a fin de inicializarlo, debemos pasarle los siguientes argumentos:
* num_inputs = número de entradas del perceptrón, en el caso de la puerta AND contamos con 2 entradas $X_0, X_1$. Esto nos permitirá inicializar los pesos de manera aleatoria. 
* lr = se refiere al learning rate, que tan rápido convergerá el perceptrón a la configuración adecuada.
* epochs = número de iteraciones en los que deseamos/esperamos que converga el perceptrón
* pesos = en casos de contar con los pesos de un perceptrón previamente entrenado, se los metemos, esto para evitar reentrenar la red.

Ahora seguiremos con las funciones de activacion más populares, ya mencionamos la función de activación de escalón sin embargo, como veremos en post posteriores esta no es utilizada, pero sirve muy bien para ejemplar el funcionamiento.

```python
  def act_fn(self, x, funcion='step'):
        """función de activación """
        if funcion == 'step':    
            return np.where(x>0, 1, 0)
        if funcion == 'sigmoid':
            return 1/(1 + np.exp(-x)) 
        if funcion == 'relu':
            return np.where(x>0, x, 0)
        if funcion == 'tanh':
            return (np.exp(x) - np.exp(-x))/(np.exp(x) + np.exp(-x))
```







