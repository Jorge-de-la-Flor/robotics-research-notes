# Cuando falla la estimación: Consecuencias a nivel de sistema en sistemas autónomos

## Introducción

En los sistemas robóticos reales, la estimación no es un componente aislado, sino una dependencia fundamental. Los errores de estimación no se limitan a un ámbito local, sino que se propagan por todo el sistema, afectando al control, la toma de decisiones y, en última instancia, a la estabilidad del sistema.

Por lo tanto, comprender los fallos en los sistemas autónomos requiere una perspectiva a nivel de sistema, no una puramente algorítmica.

---

## El fallo como propiedad del sistema

A menudo, el fallo de estimación se trata como un problema local (por ejemplo, un ajuste deficiente del filtro o una discrepancia en el modelo). Sin embargo, en la práctica, los fallos surgen de la interacción entre múltiples subsistemas.

Un sistema no falla porque un filtro sea imperfecto, sino porque la arquitectura no gestiona adecuadamente la imperfección.

---

## Mecanismos de Propagación

Los pequeños errores de estimación pueden propagarse en cascada por el sistema:

- **Representación errónea del estado →** modelo interno incorrecto de la realidad
- **Desajuste del control →** acciones basadas en suposiciones incorrectas
- **Amplificación de la retroalimentación →** errores reforzados mediante dinámicas de bucle cerrado

Esto crea condiciones en las que pequeñas imprecisiones se convierten en inestabilidad a nivel del sistema.

---

## Acoplamiento entre Estimación y Control

La estimación y el control forman un bucle estrechamente acoplado:

- Las políticas de control dependen del estado estimado
- La estimación depende de los modelos del sistema influenciados por el control

Esta interdependencia introduce un riesgo crítico:

> Los errores no solo se propagan, sino que se amplifican recursivamente.

---

## Efectos temporales y distribuidos

En sistemas distribuidos y en tiempo real, surgen modos de fallo adicionales:

- **Latencia:** las mediciones retardadas degradan la consistencia de la estimación.
- **Asincronía:** las tasas de actualización no coincidentes entre nodos.
- **Pérdida de comunicación:** estado del sistema incompleto o desactualizado.

Estos factores introducen inconsistencias que no pueden ser capturadas por modelos idealizados.

---

## Consecuencias en el mundo real

Los fallos de estimación a nivel de sistema pueden manifestarse como:

- Comportamiento de control oscilatorio o inestable.
- Falsos positivos persistentes en los sistemas de detección.
- Acciones autónomas inseguras o impredecibles.

En sistemas críticos para la seguridad, estos no son problemas de rendimiento, sino condiciones de fallo.

---

## Perspectiva de ingeniería

> La fiabilidad en los sistemas autónomos no se logra mediante una estimación perfecta, sino mediante el diseño de arquitecturas que se mantengan estables incluso con estimaciones imperfectas.

Esto replantea la estimación:

- de un objetivo → a una dependencia
- de un módulo aislado → a un factor de riesgo sistémico

---

## Principios de diseño para sistemas robustos

Para mitigar la propagación de fallos, los sistemas deben diseñarse con:

- **Estrategias de control robustas** tolerantes a errores de estimación
- **Detección redundante** para la validación cruzada del estado
- **Verificaciones de consistencia** en todos los procesos de estimación
- **Mecanismos a prueba de fallos** ante una confianza reducida

---

## Conclusión

En los sistemas autónomos, el fallo no es un evento aislado, sino una propiedad emergente de las interacciones del sistema.

Por lo tanto, el objetivo de la ingeniería no es eliminar la incertidumbre, sino diseñar sistemas en los que la incertidumbre no conduzca a un comportamiento catastrófico.
