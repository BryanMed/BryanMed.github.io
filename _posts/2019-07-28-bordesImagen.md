---
layout: post
comments: true
mathjax: true
title: 4.3| Detección de bordes en imágenes
---

Ya hablamos un poquito de la manera en la que las derivadas nos ayudan a encontrar los cambios de intensidad en señales (funciones en 1D). Ahora llegó el momento de hablar en imágenes (funciones en 2D). 

El _Gradiente_ es un vector (cuenta con _magnitud_ y _dirección_), el cual es prácticamente el equivalente a la derivación en 2 dimensiones, de hecho, está conformado por las derivadas parciales tanto de $$x$$ como en $$y$$. Recordando el [post anterior](https://bryanmed.github.io/DerivadasBordes/), vimos que la aproximación de la primera derivada en señales discretas es de la forma:

$$f'(x) = f(x + 1) - f(x)$$         --- es equivalente al kernel--->          $$[-1 \qquad 1]$$

Para formar nuestro operador de la primera derivada en una imagen $$f$$, simplemente realizamos la la diferenciación en ambas dimensiones, es así que nuestro gradiente $$\nabla f$$ queda definido como:

$$\nabla f \equiv grad(f) \equiv = 
\left[\begin{array}{cc} 
1 \\
2\\
\end{array} } \right]$$











































..

