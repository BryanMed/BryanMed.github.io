---
layout: post
comments: true
mathjax: true
title: 4.3| Detección de bordes en imágenes
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
![puenteDeFierro]({{ site.baseurl }}/images/zorroNormal.PNG) 
__Figura 1__ _Puente de Fierro, en Rioverde, SLP._

Para ello, utilizaremos los kernels de las primeras derivadas en _x_ y _y_ que mencionamos anteriormente, en la __Figura 2__ mostramos el resultado de ambas convoluciones.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/zorroNormal.PNG) 
__Figura 2__ _En la izquierda_

Antes que nada, vamos a explicar lo que significan los colores en estas imágenes. Las derivadas pueden tener valores positivos, pero también negativos, y al estar trabajando con imagenes tipo float (0.0 - 1.0), pues que onda, ¿cómo visualizamos los valores negativos (menores de cero)? para ello, Matplotlib o MATLAB realizan una adecuación de colores, asignando el color negro a la mínima intensidad y blanco al máximo, y justo en el medio, con color grisáceo está el 0. Ahora si, volvamos a discutir el resultado de la convolución, como podemos notar, al utilizar el kernel de la derivada en _x_, observamos como van apareciendo los bordes verticales (dado que estamos sacando la diferencia entre columnas), por otro lado, al utilizar el kernel de la primera derivada en _y_, notamos la formación de bordes horizontales (porque estamos diferenciando entre renglones). Para ayudar a la comprensión, en la __Figura 3__ se muestra el valor absoluto de las imágenes anteriores, en donde valores negativos o positivos se encuentran en color blanco.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/zorroNormal.PNG) 
__Figura 3__ _En la izquierda_

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

El resultado de convolucionar con ambos kernels se puede ver en la __Figura 4__ . Nótese como están caracterizados los bordes en las diagonales, en donde dependiendo del filtro que utilicemos la respuesta será más fuerte.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/zorroNormal.PNG) 
__Figura 4__ _En la izquierda_

Podemos calcular la __Magnitud $$M$$__ (que vendría siendo la _longitud_ del vector gradiente) al utilizar el resultado de ambos kernels anteriores, siguiendo la siguiente fórmula:

$$M(x, y) = mag(\nabla f) = \sqrt{g_{x}^2 + g_{y}^2}$$

No obstante, computacionalmente la raiz cuadrada es relativamente costosa, por ello, se utiliza una aproximación, que para nuestro propósito es igualmente efectiva, al utilizar el valor absoluto, de tal suerte que tenemos:

$$M(x, y) \approx |g_{x}| + |g_{y}| $$

En la __Figura 5__ y citando a Hannah Montana, vemos que _you get the best of both worlds_, teniendo bordes aún más definidos.

{: .center} 
![puenteDeFierro]({{ site.baseurl }}/images/zorroNormal.PNG) 
__Figura 5__ _En la izquierda_



































