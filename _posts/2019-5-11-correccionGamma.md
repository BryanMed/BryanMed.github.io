---
layout: post
comments: true
mathjax: true
title: 2.3| Transformación de Potencia (Corrección gama)
---

Además de la [transformación logarítmica](https://bryanmed.github.io/TransformacionLogaritmo/), existe toda una familia de funciones que se encarga de comprimir/ampliar el rango dinámico del brillo de una imagen. La _transformación de potencia_, se encuentra definida por:

{: .center}
$$g(x, y) = c \: f(x, y)^{\gamma}$$

En donde $$g(x, y)$$ corresponde a la imagen de salida, el valor de $$c$$ es una constante de escalamiento, que en este caso está definido por:

{: .center}
$$c = \frac{255}{\max(f(x, y)^{\gamma}}$$

SADASD
