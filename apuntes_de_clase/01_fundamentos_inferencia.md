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
    *   *Ejemplo:* Todos los edificios de una ciudad.
*   **Muestra (n):** Un subconjunto representativo de la población que analizamos.
    *   *Ejemplo:* Una selección aleatoria de 500 edificios.
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
    *   **Fórmula:** $$P(X=k) = p^k (1-p)^{(1-k)}$$ para k ∈ {0, 1}. Describe la probabilidad de `k` éxitos.
    *   *Ejemplo:* ¿Un edificio específico sea un edificio residencial? (Sí/No). Es la base de la Binomial.
*   **Distribución Binomial:**
    *   Describe el número de éxitos en una serie de *n* ensayos Bernoulli independientes.
    *   **Fórmula:** $$P(X=k) = C(n, k) * p^k * (1-p)^{(n-k)}$$. Probabilidad de `k` éxitos en `n` ensayos.
    *   *Ejemplo:* Si el 20% de los viajes son en bicicleta, ¿cuál es la probabilidad de que, en una muestra de 10 viajeros, exactamente 3 usen bicicleta?
*   **Distribución Geométrica:**
    *   Describe el número de ensayos de Bernoulli necesarios hasta obtener el primer éxito.
    *   **Fórmula:** $$P(X=k) = (1-p)^{(k-1)} * p$$. Probabilidad de que el primer éxito ocurra en el `k`-ésimo ensayo.
    *   *Ejemplo:* ¿Cuántos locales comerciales necesitas inspeccionar hasta encontrar el primero que no cumple la normativa de accesibilidad?
*   **Distribución de Poisson:**
    *   Modela el número de eventos que ocurren en un intervalo fijo de tiempo o espacio, dada una tasa promedio constante.
    *   **Fórmula:** $$P(X=k) = (λ^k * e^{-λ}) / k!$$. Probabilidad de `k` eventos en un intervalo, con una tasa media `λ`.
    *   *Ejemplo:* El número de accidentes de tráfico en una intersección peligrosa durante una semana.

#### Distribuciones Continuas (Resultados en un Rango)

*   **Distribución Uniforme:**
    *   Todos los resultados en un rango [a, b] son igualmente probables.
    *   **Función de Densidad (PDF):** $$f(x) = 1 / (b - a)$$ para `x` en `[a, b]`.
    *   *Ejemplo:* Si un autobús pasa cada 20 minutos, tu tiempo de espera (si llegas en un momento aleatorio) se distribuye uniformemente entre 0 y 20 minutos.
*   **Distribución Exponencial:**
    *   Describe el tiempo entre eventos en un proceso de Poisson.
    *   **Función de Densidad (PDF):** $$f(x; λ) = λ * e^{-λx}$$ para `x ≥ 0`.
    *   *Ejemplo:* El tiempo hasta que el próximo usuario llegue a una estación de bicicletas compartidas.
*   **Distribución Normal (Gaussiana):**
    *   La distribución más famosa. Simétrica, con forma de campana, definida por su media (μ) y desviación estándar (σ).
    *   **Función de Densidad (PDF):** $$f(x | μ, σ^2) = (1 / (σ * sqrt(2π))) * e^{(-(1/2) * ((x - μ) / σ)^2)}$$.
    *   Muchos fenómenos naturales y sociales la siguen.
    *   *Ejemplo:* La distribución de los precios de alquiler de apartamentos en una zona homogénea.

### 1.4 El Teorema del Límite Central (TLC)
*   **La idea central:** No importa la forma de la distribución de la población original, la distribución de las *medias muestrales* se aproximará a una distribución normal a medida que el tamaño de la muestra (n) aumenta.
*   **¿Por qué es tan importante?** Es la base de muchas pruebas de hipótesis. Nos permite hacer inferencias sobre la media de la población usando la media de nuestra muestra, incluso si no conocemos la distribución de la población.
*   **Visualización:** Lo exploraremos en el tutorial. Imaginemos tomar muchas muestras de una población, calcular la media de cada una, y luego hacer un histograma de todas esas medias. Ese histograma tendrá forma de campana.
