# Día 3: Modelos de Clasificación

**Duración:** 4 horas (2h Lectura, 2h Tutorial)

---

## Objetivos de la Sesión

*   Comprender la diferencia fundamental entre problemas de regresión (predecir un número) y clasificación (predecir una categoría).
*   Entender la intuición detrás de dos modelos de clasificación fundamentales:
    1.  **Regresión Logística:** Cómo adaptar la regresión lineal para problemas de clasificación.
    2.  **K-Vecinos más Cercanos (k-NN):** Un modelo simple basado en la "proximidad" o "similitud".
*   Aprender a dividir los datos en conjuntos de **entrenamiento y prueba** para una evaluación honesta del modelo.
*   Introducir la **matriz de confusión** como herramienta principal para evaluar el rendimiento de un clasificador.
*   Definir y entender las métricas clave de evaluación: **Precisión, Exhaustividad (Recall) y F1-Score**.
*   **Meta Práctica:** Entrenar y evaluar un modelo de Regresión Logística y un k-NN en Python.

*   Entender la intuición detrás de los **Árboles de Decisión** y cómo interpretarlos.
*   Reconocer el principal problema de los árboles de decisión: el **sobreajuste (overfitting)**.
*   Introducir los **Random Forests (Bosques Aleatorios)** como una solución al sobreajuste, basada en la "sabiduría de la multitud".
*   Comprender los conceptos de *bagging* y selección aleatoria de características.
*   **Meta Práctica:** Entrenar, visualizar y evaluar un Árbol de Decisión y un Random Forest en Python.

---

## 1. Lectura: Prediciendo Categorías

### 1.1 Qué es la Clasificación?

Hasta ahora, hemos predicho valores continuos (ej. precio de una vivienda). La clasificación se enfoca en predecir una etiqueta o categoría discreta.

*   **Clasificación Binaria:** Dos posibles resultados.
    *   *Ejemplo urbano:* Este solar es apto para construir un parque? (Sí/No)
    *   *Ejemplo urbano:* La calidad del aire en esta estación es "Buena" o "Mala"?
*   **Clasificación Multiclase:** Más de dos posibles resultados.
    *   *Ejemplo urbano:* Cuál es el uso de suelo principal de esta zona? (Residencial, Comercial, Industrial, Verde).

### 1.2 Regresión Logística

A pesar de su nombre, la Regresión Logística es un modelo de **clasificación**.

*   **La Idea Central:** En lugar de ajustar una línea recta a los datos (como en la regresión lineal), la regresión logística ajusta una **curva en forma de "S" (la función sigmoide)**.
*   **¿Cómo funciona?**
    1.  El modelo calcula una puntuación, similar a la regresión lineal.
    2.  Esta puntuación se pasa a través de la función sigmoide, que la transforma en una probabilidad entre 0 y 1.
    3.  Se establece un **umbral** (normalmente 0.5). Si la probabilidad es > 0.5, se clasifica como "Clase 1" (ej. 'Sí'); si es < 0.5, se clasifica como "Clase 0" (ej. 'No').
*   **Ventaja:** Es un modelo muy interpretable. Podemos ver cómo cada variable de entrada influye en la probabilidad del resultado.

### 1.3 K-Vecinos más Cercanos (k-NN)

k-NN es uno de los algoritmos de machine learning más simples e intuitivos.

*   **La Idea Central:** Para clasificar un nuevo punto de datos, mira a sus **'k' vecinos más cercanos** en el conjunto de datos de entrenamiento y haz que voten.
*   **¿Cómo funciona?**
    1.  Elige un valor para **'k'** (el número de vecinos a considerar, ej. k=5).
    2.  Para un nuevo punto de datos sin clasificar, mide la distancia (ej. distancia euclidiana) a todos los demás puntos.
    3.  Identifica los 'k' puntos más cercanos.
    4.  La clase que más se repite entre esos 'k' vecinos es la predicción para el nuevo punto.
*   **Importancia de 'k':**
    *   Un **'k' pequeño** (ej. k=1) hace que el modelo sea muy sensible al ruido.
    *   Un **'k' grande** hace que el modelo sea más robusto, pero puede ignorar patrones locales.
*   **Desventaja:** Puede ser computacionalmente costoso en datasets muy grandes, ya que necesita calcular la distancia a todos los puntos para cada nueva predicción. Requiere que las variables estén en una escala similar (estandarización).

### 1.4 Evaluación de Modelos: Entrenamiento y Prueba

¿Cómo sabemos si nuestro modelo es bueno? No podemos evaluarlo con los mismos datos que usamos para entrenarlo. Sería como darle a un estudiante las respuestas del examen antes de la prueba.

*   **División de Datos (Train-Test Split):**
    *   **Conjunto de Entrenamiento (Training Set):** La mayoría de los datos (ej. 80%). Se usan para que el modelo "aprenda" los patrones.
    *   **Conjunto de Prueba (Test Set):** El resto de los datos (ej. 20%). Se mantienen "ocultos" para el modelo y se usan al final para una evaluación imparcial de su rendimiento en datos nuevos.

### 1.5 La Matriz de Confusión y Métricas Clave

Para un problema de clasificación binaria, la matriz de confusión nos muestra dónde acierta y dónde se equivoca nuestro modelo.

|                | **Predicción: Positivo** | **Predicción: Negativo** |
|----------------|--------------------------|--------------------------|
| **Real: Positivo** | Verdadero Positivo (VP)  | Falso Negativo (FN)      |
| **Real: Negativo** | Falso Positivo (FP)      | Verdadero Negativo (VN)  |

*   **Verdadero Positivo (VP):** El modelo predijo 'Sí' y era 'Sí'. ¡Acierto!
*   **Falso Negativo (FN):** El modelo predijo 'No', pero era 'Sí'. ¡Error grave en algunos contextos! (ej. un test médico).
*   **Falso Positivo (FP):** El modelo predijo 'Sí', pero era 'No'. ¡Otro tipo de error! (ej. un filtro de spam que clasifica un email importante como spam).
*   **Verdadero Negativo (VN):** El modelo predijo 'No' y era 'No'. ¡Acierto!

A partir de esta matriz, derivamos métricas clave:

*   **Precisión (Precision):** De todos los que el modelo predijo como 'Positivo', ¿cuántos acertó?
    *   `Precisión = VP / (VP + FP)`
    *   Importante cuando el coste de un Falso Positivo es alto.
*   **Exhaustividad (Recall o Sensibilidad):** De todos los que eran realmente 'Positivo', ¿cuántos encontró el modelo?
    *   `Recall = VP / (VP + FN)`
    *   Importante cuando el coste de un Falso Negativo es alto.
*   **F1-Score:** La media armónica de Precisión y Recall. Un buen indicador del balance entre ambas.
    *   `F1-Score = 2 * (Precisión * Recall) / (Precisión + Recall)`

---

## 2. Lectura: Modelos Basados en Árboles

### 2.1 Árboles de Decisión

Un Árbol de Decisión es un modelo que toma decisiones haciendo una serie de preguntas simples, muy parecido a un diagrama de flujo.

*   **La Idea Central:** El algoritmo aprende una jerarquía de preguntas "si/entonces" para dividir los datos en grupos cada vez más puros.
*   **Anatomía de un Árbol:**
    *   **Nodo Raíz (Root Node):** El punto de partida, que contiene todos los datos.
    *   **División (Splitting):** El proceso de dividir un nodo en dos o más sub-nodos.
    *   **Nodo de Decisión (Decision Node):** Un sub-nodo que se divide en más sub-nodos.
    *   **Nodo Hoja (Leaf Node) o Terminal:** Un nodo que no se divide más y representa la decisión final (la clase predicha).
*   **¿Cómo aprende el árbol?**
    *   El algoritmo busca la mejor pregunta (la mejor característica y el mejor umbral) que divida los datos de la manera más "limpia" posible.
    *   "Limpieza" se mide con métricas como la **Impureza de Gini** o la **Ganancia de Información (Information Gain)**. El objetivo es que cada nodo hoja contenga, idealmente, puntos de una sola clase.
*   **Ventajas:**
    *   **Muy interpretables:** Podemos visualizar el árbol y entender exactamente las reglas que el modelo ha aprendido.
    *   No requieren escalado de variables.
*   **La Gran Desventaja: Sobreajuste (Overfitting)**
    *   Si no se controla, un árbol puede crecer hasta tener una hoja para cada punto de datos del conjunto de entrenamiento.
    *   Aprenderá el ruido de los datos de entrenamiento a la perfección, pero será incapaz de **generalizar** a datos nuevos. Un árbol muy profundo y complejo es una señal de alerta de overfitting.

### 2.2 Random Forests (Bosques Aleatorios)

Un Random Forest es un **modelo de ensamble**, lo que significa que combina las predicciones de varios modelos más simples (en este caso, árboles de decisión) para obtener una predicción final más robusta y precisa.

*   **La Idea Central:** Si un árbol de decisión es como un único experto, un Random Forest es como un comité de expertos diversos. La decisión final se toma por votación mayoritaria.
*   **¿Cómo se construye el "bosque"?** Se basa en dos ideas clave para asegurar que los árboles sean diversos:

    1.  **Bagging (Bootstrap Aggregating):**
        *   Se crean múltiples muestras del conjunto de datos de entrenamiento. Cada muestra se obtiene seleccionando puntos de datos **con reemplazo**.
        *   Esto significa que cada árbol del bosque se entrena con una versión ligeramente diferente de los datos. Algunos puntos pueden aparecer varias veces en una muestra, y otros ninguna.

    2.  **Selección Aleatoria de Características (Feature Randomness):**
        *   Al decidir cómo dividir un nodo, cada árbol no puede considerar todas las características disponibles.
        *   Solo puede elegir la mejor pregunta de un **subconjunto aleatorio** de características.
        *   Esto evita que todos los árboles se obsesionen con la misma característica predictora y fuerza al bosque a explorar diferentes patrones en los datos.

*   **Ventajas:**
    *   **Reduce drásticamente el sobreajuste** en comparación con un único árbol de decisión.
    *   Generalmente tiene un rendimiento muy alto, a menudo uno de los mejores modelos "listos para usar".
    *   Puede proporcionar **importancia de características (feature importance)**, indicando qué variables fueron más útiles para la predicción.
*   **Desventaja:**
    *   **Pérdida de interpretabilidad:** Ya no podemos visualizar una única estructura de decisión. Es una "caja negra" en comparación con un solo árbol.