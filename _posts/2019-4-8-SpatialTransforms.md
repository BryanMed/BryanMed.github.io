---
layout: post
comments: true
mathjax: true
title: 2. Transformaciones en el dominio espacial
---
## Funciones de transformación de intensidad

Este conjunto de métodos _manipula directamente_ los pixeles de la imagen, en donde estas operaciones están expresadas de la forma:

{: .center}
$$ g(x, y) = T[f(x, y)] $$

La transformación $$T$$ es básicamente una función encargada de __mapear__ las intensidades de los pixeles de entrada $$f(x, y)$$ a las de la imagen de salida $$g(x, y)$$.

Tomemos el caso mostrado en la __Gráfica 2.1__ en donde se observa la correspondencia que existe entre los niveles de intensidad de la imagen de entrada $$f(x, y)$$ es la misma respecto a aquellas en la imagen de salida $$g(x, y)$$, por lo tanto, la transformada $$T$$ en este ejemplo, es nula. Esto se observa en la __Figura 2.1__ dado que no existe diferencia alguna entre ambas imagenes debido que tienen los mismos niveles de brillo en cada pixel.

{: .center}
![grafica1]({{ site.baseurl }}/images/grafica1a1.png)

{: .center}  
__Gráfica 2.1__ _los niveles de brillo de la imagen de entrada son los mismos que los de la imagen de salida._

{: .center} 
![comparison1]({{ site.baseurl }}/images/transformada1.PNG)

{: .center}  
__Figura 2.1__ _El efecto de la transformada $$T$$ es nulo, dado que $$g(x, y) = f(x, y)$$_


## 2.1 Imagen negativa (Transformación complemento)

Este tipo de transformación es utilizada para ayudar a mejorar un poco la percepción de elementos blancos/grisáceos dentro de regiones oscuras. En esta función, se espera que los niveles de intensidad de la imagen de entrada $$f(x, y)$$, sean complementarios a aquellos en la imagen de salida. Así, al trabajar con imágenes con $$L$$ niveles de intensidad, la suma tanto del pixel de entrada, como su correspondiente en salida debe ser $$L-1$$ (dado que el rango de brillo va de $$0$$ a $$L-1$$), es decir:

{: .center}
$$f(x, y) + g(x, y) = L-1$$

Por lo tanto, el brillo que se obtiene en la imagen de salida es:

{: .center}
$$g(x, y) = L-1 - f(x, y)$$

Véase el ejemplo de la __Gráfica 2.2__ , en donde se considera que las imágenes son de formato Uint8 (256 niveles de brillo), con lo cual, la expresión queda de la siguiente manera:

{: .center}
$$g(x, y) = 255 - f(x, y)$$

{: .center} 
![graficaNegativa]({{ site.baseurl }}/images/graficaNegativa.png)

{: .center} 
__Gráfica 2.2__ _En este caso, el nivel de intensidad de entrada es el complemento del de salida, por ejemplo, si de entrada contamos con 55, a la salida obtendremos 200._

El efecto que tiene sobre las imágenes se muestra en la __Figura 2.2__ , haciendose notorio el obvio contraste entre ambas figuras. Se puede apreciar un poco mejor las lesiones dentro del pulmón en la imagen resultado de esta transformación.

{: .center} 
![pulmon]({{ site.baseurl }}/images/chest.PNG)

{: .center} 
__Figura 2.2__ _A la izquierda encontramos una imagen adquirida por rayos X, de un paciente con lesiones adquiridas por tuberculosis (Ghon's complex) y a la derecha se aprecian mejor estos detalles debido a la aplicación de la transformada complemento._

> La implementación del algoritmo de __imagen negativa__ (Python y MATLAB) la encuentras en [este](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/2.1%20imagen%20negativa) repositorio.

## 2.2 Transformación Logaritmo

No es necesario que el comportamiento de una transformación sea lineal, de hecho, muchas aplicaciones se benefician del uso de funciones no lineales, en donde mayormente se utilizan para ampliar el rango dinámico de ciertas intensidades, con el compromiso de disminuirlo en otras regiones. Por ejemplo, al aplicar la función __logaritmo__ se logra mejorar el nivel de detalle en las regiones con poco brillo, siguiendo la formula:

{: .center}
$$ g(x, y) =  c\:log(1 + f(x, y) )$$

Es necesario agregar un 1 a la función, debido a que, como se muestra en la __Gráfica 2.3__ , el logaritmo no está definido en $$0$$. Por otro lado, el valor $$c$$ es una constante que está definida por:

{: .center}
$$c = 255/log(1 + máx(f(x, y)))$$

Y la cual permite ajustar el rango de valores de salida al mismo que el de la imagen de entrada, es decir, de 0 a 255. Con ello, finalmente es posible observar el efecto de esta transformación, que, como muestra la __Figura 2.3__ es visible diferenciar con mayor detalle algunas regiones.

{: .center}
![grafica23]({{ site.baseurl }}/images/logaritmoGraph.png)

{: .center} 
__Gráfica 2.3__ Las regiones con bajo nivel de brillo, son mapeadas a un rango mas amplio de intensidades.

{: .center}
![logaritmo]({{ site.baseurl }}/images/logaritmo.png)
{: .center}
__Figura 2.3__ El efecto de la transformación logaritmo, que permite diferenciar regiones en zonas oscuras de la imagen.

> La implementación del algoritmo de __Transformación logaritmo__ (Python y MATLAB) la encuentras en [este](https://github.com/BryanMed/Procesamiento-de-imagen/tree/master/2.2%20logaritmo) repositorio.


### Referencias
+ [Capítulo 3 del libro de Digital Image Processing de Gonzalez.](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)

+ [Imagen 2.2](https://commons.wikimedia.org/wiki/File:Chest_x-ray_of_Ghon%27s_complex_of_active_tuberculosis.jpg#/media/File:Chest_x-ray_of_Ghon%27s_complex_of_active_tuberculosis.jpg)

+[Imagen 2.3](https://multimedia.larepublica.pe/660x392/larepublica/imagen/2019/04/10/noticia-1554945348-netflix.png)





