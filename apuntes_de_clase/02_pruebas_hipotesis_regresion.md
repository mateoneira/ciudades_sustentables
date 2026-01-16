# Día 2: Pruebas de Hipótesis y Regresión Lineal

**Duración:** 4 horas (2h Lectura, 2h Tutorial)

---

## Objetivos de la Sesión

*   Entender el marco de las pruebas de hipótesis: hipótesis nula, alternativa y el rol del p-valor.
*   Aprender a aplicar e interpretar tres pruebas fundamentales:
    1.  **Prueba t-Student:** para comparar las medias de dos grupos.
    2.  **Prueba Chi-cuadrado (χ²):** para evaluar la relación entre dos variables categóricas.
    3.  **Análisis de Correlación:** para medir la fuerza y dirección de una relación lineal entre dos variables continuas.
*   Comprender la diferencia clave entre correlación y causalidad.
*   Introducir el modelo de Regresión Lineal Simple como una herramienta para explicar y predecir.
*   **Meta Práctica:** Ser capaz de realizar pruebas de hipótesis y ajustar un modelo de regresión lineal simple en Python.

---

## 1. Lectura: De la Inferencia a la Explicación

### 1.1 La Prueba de Hipótesis

La prueba de hipótesis es un procedimiento formal para tomar decisiones basadas en datos en un contexto de incertidumbre.

1.  **Formular la Hipótesis Nula (H₀):** Es la afirmación escéptica, el "statu quo". Generalmente postula que "no hay efecto" o "no hay diferencia".
    *   *Ejemplo:* No hay diferencia en el precio medio de los alquileres entre la Zona A y la Zona B.
2.  **Formular la Hipótesis Alternativa (H₁):** Es la afirmación que queremos probar. Postula que "hay un efecto" o "hay una diferencia".
    *   *Ejemplo:* El precio medio de los alquileres es diferente entre la Zona A y la Zona B.
3.  **Calcular un Estadístico de Prueba:** Un valor calculado a partir de nuestra muestra que mide qué tan lejos están nuestros datos de lo que esperaríamos si la hipótesis nula fuera cierta.
4.  **Calcular el p-valor:** La probabilidad de observar un resultado tan extremo (o más extremo) como el de nuestra muestra, *asumiendo que la hipótesis nula es verdadera*.
5.  **Tomar una Decisión:**
    *   Si el **p-valor es pequeño** (típicamente < 0.05), "rechazamos la hipótesis nula". La evidencia sugiere que H₀ es improbable.
    *   Si el **p-valor es grande** (≥ 0.05), "no podemos rechazar la hipótesis nula". No tenemos suficiente evidencia para descartarla. ¡Ojo! Esto no significa que H₀ sea verdadera.

### 1.2 Pruebas Estadísticas Clave

*   **Prueba t-Student (para medias):**
    *   **Pregunta:** ¿Son significativamente diferentes las medias de dos grupos?
    *   **Variables:** Una variable numérica (ej. precio alquiler) y una variable categórica con dos niveles (ej. Zona A, Zona B).
    *   **Resultado:** Un p-valor que nos dice si la diferencia observada en las medias de las muestras es estadísticamente significativa.

*   **Prueba Chi-cuadrado (χ²) (para independencia):**
    *   **Pregunta:** ¿Están relacionadas dos variables categóricas?
    *   **Variables:** Dos variables categóricas (ej. "Tipo de barrio" y "Acceso a parque").
    *   **Idea:** Compara las frecuencias que observamos en nuestra muestra con las frecuencias que esperaríamos si las dos variables fueran totalmente independientes.
    *   **Resultado:** Un p-valor que nos dice si la asociación observada es estadísticamente significativa.

*   **Análisis de Correlación (para variables continuas):**
    *   **Pregunta:** ¿Cómo se mueven juntas dos variables numéricas?
    *   **Variables:** Dos variables numéricas (ej. "tamaño del apartamento en m²" y "precio del alquiler").
    *   **Coeficiente de Correlación (r):** Un valor entre -1 y 1.
        *   **r ≈ 1:** Correlación positiva fuerte (si una sube, la otra también).
        *   **r ≈ -1:** Correlación negativa fuerte (si una sube, la otra baja).
        *   **r ≈ 0:** No hay correlación lineal.

### 1.3 Correlación no implica Causalidad

Este es un concepto fundamental en la ciencia de datos. Que dos variables estén correlacionadas no significa que una cause la otra. Puede haber una **variable de confusión** (o variable latente) que explique la relación.

*   *Ejemplo Clásico:* Hay una fuerte correlación positiva entre la venta de helados y los ataques de tiburón.
*   *¿Causa?:* No, la venta de helados no causa los ataques. La variable de confusión es la **temperatura / temporada de verano**. Más calor lleva a más gente a la playa (más ataques) y a más gente a comprar helados.

### 1.4 Introducción a la Regresión Lineal Simple

Mientras que la correlación solo nos dice la fuerza y dirección de una relación, la regresión nos permite **modelarla**.

*   **Objetivo:** Encontrar la línea recta que mejor se ajusta a la nube de puntos de nuestros datos.
*   **Ecuación:** **Y = β₀ + β₁X + ε**
    *   **Y:** Variable dependiente (la que queremos predecir, ej. precio).
    *   **X:** Variable independiente (la que usamos para predecir, ej. tamaño).
    *   **β₀:** Intercepto (el valor de Y cuando X es 0).
    *   **β₁:** Coeficiente o pendiente (cuánto cambia Y por cada unidad que aumenta X).
    *   **ε:** El error o residuo (la parte de Y que el modelo no puede explicar).
*   **Interpretación:** El coeficiente **β₁** es clave. Nos dice el efecto estimado de X sobre Y.
*   **Evaluación del Modelo (R²):** El "coeficiente de determinación" nos dice qué porcentaje de la variabilidad de Y es explicado por nuestro modelo (por X). Un R² de 0.70 significa que el 70% de la variación en los precios de alquiler se explica por el tamaño de los apartamentos.

---

