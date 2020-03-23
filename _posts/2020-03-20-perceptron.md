---
layout: post
comments: true
mathjax: true
title: ML-1| Percetrón
---
> La implementación del perceptrón en python la encuentras en [este repositorio](https://github.com/BryanMed/ML-Blog/tree/master/Perceptron). Para que corras este código de manera interactiva sin la necesidad de instalar nada, puedes correr la siguiente notebook [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BryanMed/ML-Blog/blob/master/Perceptron/perceptron.ipynb)

¡Hola! después de un tiempito, publicaré algunos posts enfocados en el Machine Learning, quiero agradecer al [Dr. Onofre Orozco](https://www.researchgate.net/profile/Onofre_Orozco) por su apoyo y explicaciones en estos temas. 

El objetivo de estos posts es hacerlos un poco más interactivos, es por ello que publicaré una versión del código en Google Colab (una jupyter notebook) para que puedas correr las implementaciones sin instalar nada en tu pc, solo necesitas contar con internet y tu cuenta de Gmail. 

# La Neurona biológica

La unidad principal del sistema nervioso central, y se encarga de **recibir**, **procesar** y **transmitir** información a través de señales electroquímicas. Estas características en su funcionamiento despertarón el interés para crear un modelo que emulara este comportamiento. En la siguiente imagen podemos observar un modelo de una neurona, en donde discutiremos la función de algunas de sus partes que más llaman nuestro interés.

![neurona]({{ site.baseurl }}/images/ML1 perceptron//neurona.PNG)
> *neurona biológica, fotografía tomada de la [wiki](https://commons.wikimedia.org/wiki/File:Neurons_uni_bi_multi_pseudouni.svg)*

* **Dendritas:** Son las pequeñas ramificaciones que se encuentran en el soma, y su importancia recae en que su función principal es el recibir estimulos nerviosos provenientes de otras neuronas (sinápsis), y enviarlas al soma. Es importante considerar que no todos los impulsos de las neuronas que conectan con las dendritas tienen la misma intensidad, siendo determinado por distintos factores como la mielización de la neurona pre-sináptica (que tan bien se propaga la señal en el axón), cantidad de neurontransmisor, el número de conexiones del axón con las dendrítas, entre otros. 

* **Soma :** Es el cuerpo celular de la neurona, en donde se encuentra el citoplasma y otros orgánelos de gran importancia que se encargan de regir el funcionamiento y mantener con vida la unidad biológica. De entre las muchas funciones del soma, las que más nos interesan son: Que aquí se lleva a cabo la mayor parte de síntesis de las proteínas, en las que algunas son parte o promueven la creación de **neurontransmisores**. Es aquí donde se lleva a cabo el procesamiento de la información nerviosa y su reacción a ella.

* **Axón :** Es la gran prolongación/brazo que sale desde desde el soma, y es, de manera general, el encargado de la transmisión del impulso eléctrico, no obstante, para que se pueda generar este **Potencial de acción**, se tiene que superar un umbral de despolarización, el cual se logra en dos casos, 1) al llegar un estímulo lo suficientemente grande, o 2) la suma de varios estímulos dentro de un corto periodo de tiempo. Al superar este umbral, la neurona se "dispara" llegando la señal eléctrica al botón terminal, que será la señal de liberación de partículas químicas que llegarán a la neurona post-sináptica. _Transmitiendo una señal_.

# El Perceptrón 

Es básicamente una representación matemática muy burda del funcionamiento de la neurona biológica, que, en solitario, permite la resolución de problemas linealmente separables (más de esto más adelante, pero son aquellos problemas en los que podemos separar distintos grupos mediante lineas rectas). En el siguiente diagrama podemos observar una representación de este modelo y como trata de emular la estructura de la neurona. 

![perceptron]({{ site.baseurl }}/images/ML1 perceptron//perceptron.PNG)
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

![step]({{ site.baseurl }}/images/ML1 perceptron//step.PNG)
> *Función de activación de escalón unitario*

Finalmente podemos representar la señal de salida de la neurona mediante $\hat y$.

$$\hat y = \phi (w^{T}\cdot x - \theta) $$ 


# Entrenamiento 

Hasta el momento ya contamos con un perceptrón, pero dado que los pesos normalmente se inicializan con ceros o valores aleatorios, es muy improbable que esta neurona sea capaz de predecir correctamente una salida que nosotros esperemos. Y esto es porque el perceptrón aún no ha sido entrenado. 

Pensemos en como nosotros como humanos aprendemos a realizar una tarea, digamos aprender a escribir. Al darnos papel y lápiz por primera vez, probablemente lo primero que hagamos será tomar el lápiz y meterlo a la boca o nariz, pero bueno, una vez que nuestros padres nos muestren lo que deberíamos de hacer con estas herramientas empezaremos a garabatear, después trataremos de aprender una tarea más compleja que es aprender a escribir, para ello nos tratarán de enseñar con el ejemplo "este círculo y rayita forman una aaaaaa", y nosotros empezaremos a perfeccionar la técnica para crear una "a", sin embargo, en un inicio no seremos lo suficientemente hábiles para lograrlo a la primera, y cometeremos muchísimos *errores* y a partir de estos seremos capaces de mejorar.

Este mismo proceso se aplica a las redes neuronales. Pensemos en el perceptrón como un empleado al cual le asignaremos una tarea y lo vamos a capacitar para que la realice apropiadamente, nuestra conversación sería algo más o menos así:

Yo: "mira, el usuario va a ingresar estas entradas, ¿cuál va a ser tu salida?"
perci: "ok, de acuerdo a esas entradas yo voy a generar esta salida"
yo: "muy bien, pero mira esto es lo que yo esperaría que obtuvieras, así que vamos a comparar"

La mejor manera de comparar es viendo la **diferencia** entre ambas salidas, literalmente vamos a restar el valor arrojado por el perceptrón con el que nosotros esperaríamos. Y aquí hay de dos sopas, si la diferencia es nula el empleado perci realizó bien su tarea, pero si llega a existir diferencia la neurona no cumplió el objetivo, y por ello debemos capacitarla nuevamente, pero antes de eso debemos de tomar en cuenta esa equivocación, por lo que basado en el error modificaremos las herramientas con las que produce la salida y estas son los pesos sinápticos, permitiendo al perceptrón aprender de su error.

A esta manera de aprender se le conoce como la **Delta Rule** debido a que, en caso de que la predicción sea erronea, se realizará un ajusto de pesos y bias al agregarles un pequeño ajuste (un Delta $\Delta$) de la siguiente manera:

bias: $$ w_0 = w_0 + lr * error $$

pesos sinápticos: $$ w_i = w_i + lr * error * x_i$$ 

En donde $lr$ se refiere al *learning rate* y es un factor que indica que tan rápido o lento convergerá el perceptrón a una solución (con el respectivo *tradeoffs* de valocidad-convergencia), normalmente este parámetro se inicializa con 0.2.

Finalmente podemos pasar a la implementación de este algoritmo.

---

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
Quizá más adelante discuta sus propiedades, mientras tanto en la siguiente figura se muestran las funciones de activación implementadas.

![funciones](actfun.PNG)
> *Funciones de activación de escalón unitario, sigmoide, ReLu, tanh*

La siguiente función que nos interesa es el feedforward, es decir, el producto punto de las entradas con los pesos sinápticos al que restaremos el bias.

```python    
def predict(self, inputs):
        """feedforward del perceptron"""
        return self.act_fn(np.dot(inputs, self.weights[1:]) + self.weights[0])
```
A esta función la llamé `predict`, porque es la encargada de realizar la predicción ja.Es decir, nosotros ingresamos un conjunto de entradas, y de acuerdo a estas el perceptrón arrojará una salida.

Ahora viene la parte del `entrenamiento`:

```python
def train(self, in_train, clases, verbose=False):
        """entrenamiento del perceptron"""
        errores = []
        for _ in range(self.epochs):
            e = 0
            for entrada, clase in zip(in_train, clases):
                prediccion = self.predict(entrada)
                error = clase - prediccion
                self.weights[0] += self.lr * error
                self.weights[1:] += self.lr * error * entrada
            
                e += np.abs(error)   
            errores.append(e)
```
en donde los argumentos `in_train` se refiere a las entradas, `clases` a las salidas esperadas/labels y `verbose` sirve mostrar los errores que ha tenido el perceptrón en cada época. Dentro de la función realiza el ajuste del bias y pesos y esto se realiza hasta iterar "epocas" veces.

Finalmente `get_weights` nos permite recuperar los pesos actuales del perceptrón, lo cual es útil cuando queremos guardar los pesos de la red una vez que esté entrenada y así evitar el proceso de entrenamiento cada vez que corramos el programa.

```python
  def get_weights(self):
        """recupero los pesos de la red, útil para no volver a entrenar"""
        return self.weights
```
> Para que puedas experimentar con la explicación del código anterior, te recomiendo que veas la notebook siguiente [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BryanMed/ML-Blog/blob/master/Perceptron/perceptron.ipynb)











