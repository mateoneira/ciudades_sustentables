# Día 1: Fundamentos de Inferencia

**Duración:** 4 horas (2h Lectura, 2h Tutorial)

---

## Objetivos de la Sesión

*   Comprender la diferencia entre población y muestra y la importancia del muestreo en la ciencia de datos.
*   Entender los conceptos básicos de probabilidad y su aplicación en la toma de decisiones.
*   Familiarizarse con las distribuciones de probabilidad más comunes (Bernoulli, Binomial, Geometric, Poisson, Uniform, Normal, Exponential).
*   Visualizar y comprender el Teorema del Límite Central a través de simulaciones.
*   **Meta Práctica:** Ser capaz de generar datos simulados y visualizar distribuciones en Python.

---

## 1. Lectura: Conceptos Fundamentales (2 horas)

### 1.1 De la Población a la Muestra
*   **Población (N):** El universo completo de datos o individuos sobre el que queremos sacar conclusiones.
    *   *Ejemplo urbano:* Todos los edificios de una ciudad.
*   **Muestra (n):** Un subconjunto representativo de la población que analizamos.
    *   *Ejemplo urbano:* Una selección aleatoria de 500 edificios.
*   **¿Por qué muestrear?** Es a menudo imposible o demasiado costoso analizar a toda la población.
*   **Inferencia:** El proceso de usar la información de la muestra para hacer afirmaciones (inferir) sobre la población.

### 1.2 Fundamentos de Probabilidad
*   **Probabilidad:** La medida de la certidumbre de que un evento ocurra. Varía entre 0 (imposible) y 1 (seguro).
*   **Conceptos Clave:**
    *   **Experimento:** Una acción con un resultado incierto (lanzar un dado).
    *   **Espacio Muestral:** Todos los resultados posibles ({1, 2, 3, 4, 5, 6}).
    *   **Evento:** Un resultado específico de interés (que salga un número par).
*   **Relevancia para Datos:** La probabilidad nos ayuda a cuantificar la incertidumbre en nuestros modelos y conclusiones.

### 1.3 Distribuciones de Probabilidad
*   Una función que describe la probabilidad de todos los resultados posibles de una variable. Se dividen en discretas (números contables) y continuas (cualquier valor en un rango).

#### Distribuciones Discretas (Resultados Contables)

*   **Distribución Bernoulli:**
    *   Representa un único experimento con dos posibles resultados: éxito (1) o fracaso (0).
    *   *Ejemplo urbano:* ¿Un edificio específico cumple con el código de sismicidad? (Sí/No). Es la base de la Binomial.
*   **Distribución Binomial:**
    *   Describe el número de éxitos en una serie de *n* ensayos Bernoulli independientes.
    *   *Ejemplo urbano:* Si el 20% de los viajes son en bicicleta, ¿cuál es la probabilidad de que, en una muestra de 10 viajeros, exactamente 3 usen bicicleta?
*   **Distribución Geométrica:**
    *   Describe el número de ensayos de Bernoulli necesarios hasta obtener el primer éxito.
    *   *Ejemplo urbano:* ¿Cuántos locales comerciales necesitas inspeccionar hasta encontrar el primero que no cumple la normativa de accesibilidad?
*   **Distribución de Poisson:**
    *   Modela el número de eventos que ocurren en un intervalo fijo de tiempo o espacio, dada una tasa promedio constante.
    *   *Ejemplo urbano:* El número de accidentes de tráfico en una intersección peligrosa durante una semana.

#### Distribuciones Continuas (Resultados en un Rango)

*   **Distribución Uniforme:**
    *   Todos los resultados en un rango [a, b] son igualmente probables.
    *   *Ejemplo urbano:* Si un autobús pasa cada 20 minutos, tu tiempo de espera (si llegas en un momento aleatorio) se distribuye uniformemente entre 0 y 20 minutos.
*   **Distribución Exponencial:**
    *   Describe el tiempo entre eventos en un proceso de Poisson.
    *   *Ejemplo urbano:* El tiempo hasta que el próximo usuario llegue a una estación de bicicletas compartidas.
*   **Distribución Normal (Gaussiana):**
    *   La distribución más famosa. Simétrica, con forma de campana, definida por su media (μ) y desviación estándar (σ).
    *   Muchos fenómenos naturales y sociales la siguen.
    *   *Ejemplo urbano:* La distribución de los precios de alquiler de apartamentos en una zona homogénea.

### 1.4 El Teorema del Límite Central (TLC)
*   **La idea central:** No importa la forma de la distribución de la población original, la distribución de las *medias muestrales* se aproximará a una distribución normal a medida que el tamaño de la muestra (n) aumenta.
*   **¿Por qué es tan importante?** Es la base de muchas pruebas de hipótesis. Nos permite hacer inferencias sobre la media de la población usando la media de nuestra muestra, incluso si no conocemos la distribución de la población.
*   **Visualización:** Lo exploraremos en el tutorial. Imaginemos tomar muchas muestras de una población, calcular la media de cada una, y luego hacer un histograma de todas esas medias. Ese histograma tendrá forma de campana.

---

## 2. Tutorial: Simulación en Python (2 horas)

*   **Herramientas:** Jupyter Notebook, `numpy`, `matplotlib`, `seaborn`.
*   **Actividades:**
    1.  **Simulación de Distribuciones Discretas:** Binomial y Poisson.
    2.  **Simulación de Distribuciones Continuas:** Normal y Exponencial.
    3.  **Demostración Práctica del TLC:**
        *   Crear una población con una distribución no normal (ej. uniforme o exponencial).
        *   Tomar múltiples muestras de esta población.
        *   Calcular la media de cada muestra.
        *   Crear un histograma de las medias muestrales para observar cómo se aproxima a la normalidad.

