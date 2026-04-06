# Fallo en la estimación ante discrepancias en el modelo: Una observación práctica

## Resumen

Las técnicas de estimación de estado, como el filtro de Kalman, presuponen modelos de sistema precisos y ruido bien caracterizado. En sistemas embebidos reales, estas suposiciones rara vez se cumplen.

Esta nota documenta una observación práctica: cómo pequeñas discrepancias entre el modelo supuesto y el sistema real pueden degradar la calidad de la estimación y provocar un comportamiento inestable del sistema.

---

## Contexto experimental

La observación se basa en un sistema de detección distribuido compuesto por:

- Un nodo de detección basado en Arduino
- Mediciones de distancia ultrasónicas (HC-SR04)
- Un filtro de Kalman 1D implementado en el dispositivo
- Transmisión a través de UART → MQTT → nodo de borde

El sistema opera en condiciones reales, incluyendo ruido del sensor, variabilidad de temporización y retrasos en la comunicación.

---

## Supuestos del modelo

El filtro de Kalman se implementó bajo supuestos estándar:

- Transición de estado lineal
- Ruido de medición gaussiano
- Ruido de proceso (Q) y ruido de medición (R) fijos

Estos supuestos simplifican el problema de estimación, pero introducen riesgos cuando no se ajustan a la realidad.

---

## Discrepancias observadas

En la práctica, se observaron varias desviaciones:

- El ruido del sensor ultrasónico presentó un comportamiento no gaussiano (picos y valores atípicos)
- La latencia de medición varió según la carga del sistema
- Los factores ambientales afectaron la consistencia de la señal

Estos efectos violan los supuestos fundamentales del filtro de Kalman.

---

## Comportamiento ante fallos

En estas condiciones, se observaron los siguientes comportamientos:

- **Suavizado excesivo:** El filtro se retrasó con respecto a los cambios rápidos de distancia.
- **Respuesta retardada:** Las actualizaciones de estado no se alinearon con la dinámica en tiempo real.
- **Divergencia transitoria:** Los picos repentinos de medición provocaron una deriva temporal en la estimación.

Estos efectos no fueron constantes, sino que aparecieron bajo condiciones operativas específicas.

---

## Impacto a nivel de sistema

Los errores de estimación se propagaron al comportamiento del sistema:

- Clasificación incorrecta de la proximidad en la máquina de estados finitos.
- Transiciones retardadas entre los estados del sistema.
- Actuación inconsistente (respuestas de servo y alerta).

Esto demuestra que los errores de estimación influyen directamente en la lógica de control y en los resultados del sistema.

---

## Perspectiva de ingeniería

> La calidad de la estimación no puede evaluarse de forma aislada del comportamiento del sistema.

Un filtro que parece estable de forma aislada puede producir resultados indeseables al integrarse en un sistema real con restricciones de tiempo y lógica de decisión.

---

## Ajustes prácticos

Para mitigar estos efectos, se consideraron varios ajustes:

- Aumentar el ruido de medición (R) para reducir el exceso de confianza.
- Introducir validación basada en umbrales para el rechazo de valores atípicos.
- Diseñar transiciones de máquinas de estados finitos (FSM) para tolerar el retardo de estimación.

Estos ajustes mejoraron la robustez del sistema sin necesidad de un cambio completo en el método de estimación.

---

## Conclusión

Esta observación destaca un principio clave en robótica:

La estimación no es una solución aislada, sino un componente cuyo comportamiento debe evaluarse dentro del sistema completo.

Los sistemas fiables no surgen de modelos perfectos, sino de arquitecturas que se mantienen estables incluso cuando los modelos son imperfectos.
