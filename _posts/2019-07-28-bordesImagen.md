---
layout: post
comments: true
mathjax: true
title: 4.3| Detección de bordes en imágenes - Roberts y Prewitt
---

Ya hablamos un poquito de la manera en la que las derivadas nos ayudan a encontrar los cambios de intensidad en señales (funciones en 1D). Ahora llegó el momento de hablar en imágenes (funciones en 2D). 

El _Gradiente_ es un vector (cuenta con _magnitud_ y _dirección_), el cual es prácticamente el equivalente a la derivación en 2 dimensiones, de hecho, está conformado por las derivadas parciales tanto de $$x$$ como en $$y$$. Recordando el [post anterior](https://bryanmed.github.io/DerivadasBordes/), vimos que la aproximación de la primera derivada en señales discretas es de la forma:

$$f'(x) = f(x + 1) - f(x) \qquad$$         --- es equivalente al kernel--->          $$\qquad [-1 \qquad 1]$$

Para formar nuestro operador de la primera derivada en una imagen $$f$$, simplemente realizamos la la diferenciación en ambas dimensiones, es así que nuestro gradiente $$\nabla f$$ queda definido como:

$$\nabla f \equiv grad(f) = 
\left[ \begin{array}{cc} 
g_{x} \\
g_{y}\\
\end{array} \right] = 
\left[ \begin{array}{cc}
\frac{\partial f}{\partial x}\\ \\
\frac{\partial f}{\partial y}\\
\end{array} \right]
$$

Las máscaras que corresponden a estas derivadas, son las siguientes:

kernel de la 1a derivada en x: $$[-1 \qquad 1]$$

kernel de la 1a derivada en y:
$$\left[ \begin{array}{cc}
-1 \\
1\\
\end{array} \right]
$$

Ahora vamos a realizar la detección de bordes en la imagen de la __Figura 1__.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/puenteDeFierro.PNG) 
__Figura 1__ _Puente de Fierro, en Rioverde, SLP. [créditos](https://commons.wikimedia.org/wiki/File:Puente_de_Fierro_de_Rioverde_SLP.JPG)_

Para ello, utilizaremos los kernels de las primeras derivadas en _x_ y _y_ que mencionamos anteriormente, en la __Figura 2__ mostramos el resultado de ambas convoluciones.

{: .center} 
![derx2]({{ site.baseurl }}/images/PuenteDerivadaXY.PNG) 
__Figura 2__ _En la izquierda encontramos el resultado de la convolución utilizando el kernel de la primera derivada en el eje x, a la derecha utilizando la derivada en el eje y_

Antes que nada, vamos a explicar lo que significan los colores en estas imágenes. Las derivadas pueden tener valores positivos, pero también negativos, y al estar trabajando con imagenes tipo float (0.0 - 1.0), pues que onda, ¿cómo visualizamos los valores negativos (menores de cero)? para ello, Matplotlib o MATLAB realizan una adecuación de colores, asignando el color negro a la mínima intensidad y blanco al máximo, y justo en el medio, con color grisáceo está el 0. Ahora si, volvamos a discutir el resultado de la convolución, como podemos notar, al utilizar el kernel de la derivada en _x_, observamos como van apareciendo los bordes verticales (dado que estamos sacando la diferencia entre columnas), por otro lado, al utilizar el kernel de la primera derivada en _y_, notamos la formación de bordes horizontales (porque estamos diferenciando entre renglones). Para ayudar a la comprensión, en la __Figura 3__ se muestra el valor absoluto de las imágenes anteriores, en donde valores negativos o positivos se encuentran en color blanco.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/PuenteDerivadaXYAbs.PNG) 
__Figura 3__ _Se muestra el valor absoluto de los bordes detectados con las derivadas en los ejes x y y de la __Figura 2__ _

Entre los inconvenientes que se tiene al utilizar estos detectores, es que al momento de encontrar bordes diagonales pues la cosa ya no funcionaba tan bien. Uno de las primeras intentos por crear un kernel que priorizara los bordes diagonales, es el _filtro Roberts_, en donde se realiza la diferenciación en direcciones precisamente diagonales, cuyas máscaras se muestran a continuación:

$$g_{x} = 
\left[ {\begin{array}{cccc}
-1 & 0 \\
0 & 1 \\
\end{array} } \right]
$$

$$g_{y} = 
\left[ {\begin{array}{cccc}
0 & -1 \\
1 & 0 \\
\end{array} } \right]
$$

El resultado de convolucionar con ambos kernels se puede ver en la __Figura 4__, en la __Figura 5__ se muestra el valor absoluto de ambas imágenes. Nótese como están caracterizados los bordes en las diagonales, en donde dependiendo del filtro que utilicemos la respuesta será más fuerte.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/PuenteRoberts.PNG) 
__Figura 4__ _Resultado de la convolución, utilizando operadores que hacen más fuerte la respuesta en direcciones diagonales, nótese la diferencia de dirección en ambas imágenes._

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/PuenteRobertsAbs.PNG) 
__Figura 5__ _Valor absoluto de las imágenes de la __Figura 4__ _

Podemos calcular la __Magnitud $$M$$__ (que vendría siendo la _longitud_ del vector gradiente) al utilizar el resultado de ambos kernels anteriores, siguiendo la siguiente fórmula:

$$M(x, y) = mag(\nabla f) = \sqrt{g_{x}^2 + g_{y}^2}$$

No obstante, computacionalmente la raiz cuadrada es relativamente costosa, por ello, se utiliza una aproximación, que para nuestro propósito es igualmente efectiva, al utilizar el valor absoluto, de tal suerte que tenemos:

$$M(x, y) \approx |g_{x}| + |g_{y}| $$

En la __Figura 6__ y citando a Hannah Montana, vemos que _you get the best of both worlds_, teniendo bordes aún más definidos. Además para hacer más notorios los bordes, podemos binarizar la imagen, definiendo cierto _umbral_, en el que si un pixel llega a superarlo, se le asignará un valor de 1 (blanco) y de no hacerlo, se le asigna un 0 (negro). 

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/PuenteRobertsMag.PNG) 
__Figura 6__ _En la izquierda encontramos la magnitud del gradiente de la imagen, a la derecha vemos la imagen binarizada cuyo umbral a superar es del 10% del máximo valor de magnitud encontrado en la imagen._

Como ya mencionamos en el post de convolución, en el caso de imágenes es preferible trabajar con kernels de número impar, ya que son simétricas respecto a un punto central. Una ventaja con los kernels impares, es que permiten comparar mejor entre los lados opuestos respecto al centro de este. En señales, para conseguir dicha función, utilizamos la siguiente máscara:

$$w = [-1 \qquad 0 \qquad 1] $$

El _filtro Prewitt_ es  una extensión de esta idea en dos dimensiones, con lo cual se obtiene los siguientes filtros para detectar bordes en los ejes _x_ y _y_, además, en las __Figura 7 - 8__ encontramos el resultado de la convolución con estos operadores.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/piso.jpg) 
__Figura 7__ _Piso de las tortas alemanas (enfrente de ciencias químicas de la UASLP)._

$$
Prewitt_{x} = \begin{vmatrix}
-1&-1&-1\\
0&1&0\\
1&1&1\\
\end{vmatrix}

\qquad

Prewitt_{y} = \begin{vmatrix}
-1&0&1\\
-1&0&1\\
-1&0&1\\
\end{vmatrix}
$$

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/PrewittDXY.PNG) 
__Figura 8__ _Valor absoluto del resultado de la convolución con sus respectivos filtros Prewitt (en _x_ y _y_, para detectar bordes en dirección horizonal y vertical_

De igual manera, también podemos priorizar los bordes en diagonal, y en la __Figura 9__ se muestra los bordes detectados por estos operadores.

$$
Prewitt_{d1} = \begin{vmatrix}
 0&  1&  1\\
-1&  0&  1\\
-1& -1&  0\\
\end{vmatrix}

\qquad

Prewitt_{d2} = \begin{vmatrix}
 -1& -1&  0\\
 -1&  0&  1\\
  0&  1&  1\\
\end{vmatrix}
$$

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/PrewittD12.PNG) 
__Figura 9__ _Valor absoluto del resultado de la convolución con sus respectivos filtros Prewitt (_diagonal 1 - diagonal 2_), para detectar bordes en direcciónes diagonales._

Finalmente en la __Figura 10__ mostramos la magnitud y a su vez, la versión binarizada de esta imagen.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/PrewittMag.PNG) 
__Figura 10__ _A la izquierda vemos la imagen correspondiente a la magnitud del gradiente, por el otro lado, encontramos esta imagen binarizada con un umbral del 10%._

Si bien muchos de los bordes son detectados, también puntos o líneas no deseadas son detectadas. Esto es un efecto no deseado, en el siguiente post hablaremos de un filtro más choncho, el _operador Sobel_ y hablaremos de los efectos que tiene el ruido en la detección de bordes.

> El código para detectar bordes utilizando los operadores Roberts y Prewitt lo encuentras en [este](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/4.3%20detector%20de%20bordes%20imagenes%20-%20roberts%20y%20prewitt) repositorio.

______

### Referencias

* [Capítulo 10 del libro de Gonzalez](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)























