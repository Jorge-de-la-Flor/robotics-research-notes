# Limitaciones del filtro de Kalman en sistemas reales

## Introducción

El filtro de Kalman se utiliza ampliamente para la estimación de estado en robótica debido a su optimalidad bajo supuestos lineales gaussianos. Sin embargo, los sistemas reales rara vez cumplen estos supuestos a la perfección. Comprender sus limitaciones es esencial para diseñar sistemas autónomos fiables.

---

## Supuestos y violaciones prácticas

El filtro de Kalman estándar se basa en varios supuestos clave:

- Dinámica lineal del sistema
- Distribuciones de ruido gaussiano
- Modelos precisos del sistema y del ruido

En la práctica, estos supuestos suelen incumplirse:

- **Dinámica no lineal:** Los sistemas robóticos reales suelen presentar un comportamiento no lineal, especialmente en el movimiento y la detección.

- **Ruido no gaussiano:** El ruido del sensor puede incluir valores atípicos, sesgos o distribuciones de cola pesada.

- **Desajuste del modelo:** Los modelos de sistema imprecisos pueden provocar divergencias con el tiempo.

---

## Modos de fallo observados en la práctica

Mediante implementaciones experimentales con datos de sensores ruidosos, se observan varios patrones de fallo:

- **Divergencia del filtro:** Cuando el modelo es incorrecto o el ruido se subestima, la estimación se desvía de la realidad.

- **Exceso de confianza:** Un ajuste deficiente de la covarianza produce estimaciones que parecen certeras, pero que son incorrectas.

- **Sensibilidad a la latencia:** Las mediciones retardadas pueden desestabilizar la estimación si no se gestionan adecuadamente.

- **Inconsistencia del sensor:** Las entradas de sensores contradictorias pueden degradar la calidad de la estimación si no se ponderan correctamente.

---

## Implicaciones de ingeniería

Estas limitaciones ponen de manifiesto un principio importante:

> La estimación de estado no es solo un problema matemático, sino un desafío de ingeniería de sistemas.

La estimación robusta requiere:

- Modelado cuidadoso de las características del sistema y del ruido
- Validación continua de las suposiciones
- Integración con las restricciones del sistema, como la temporización, la comunicación y la computación

---

## Extensiones y alternativas

Para abordar estas limitaciones, se suelen utilizar varios enfoques:

- **Filtro de Kalman extendido (EKF):** Maneja no linealidades leves mediante linealización
- **Filtro de Kalman sin aroma (UKF):** Mejora la estimación bajo transformaciones no lineales
- **Filtros de partículas:** Adecuado para sistemas altamente no lineales y no gaussianos

---

## Conclusión

En robótica real, el filtro de Kalman no es una solución universal, sino un componente dentro de una arquitectura de estimación más amplia. La autonomía fiable depende de comprender cuándo funciona el filtro, cuándo falla y cómo interactúa con las restricciones físicas y computacionales.
