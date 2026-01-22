# Redes Neuronales

## 1. Inspiración Biológica: El Cerebro

Las redes neuronales artificiales (ANNs) se inspiran en la estructura y funcionamiento del cerebro humano. El cerebro está compuesto por miles de millones de neuronas interconectadas que procesan información en paralelo. Cada neurona recibe señales, las procesa y transmite una nueva señal a otras neuronas.

## 2. El Bloque Fundamental: La Neurona Artificial (Perceptrón)

La unidad más básica de una red neuronal es una neurona artificial, también conocida como **perceptrón**.

Una neurona:
1.  **Recibe entradas (inputs):** Cada entrada `x_i` tiene un **peso (weight)** asociado `w_i`. El peso determina la importancia de esa entrada.
2.  **Calcula una suma ponderada:** Se multiplican todas las entradas por sus pesos y se suman. A esto se le añade un **sesgo (bias)** `b`. El sesgo actúa como un intercepto, permitiendo ajustar la salida independientemente de las entradas.
    *   `Suma = (x_1 * w_1) + (x_2 * w_2) + ... + (x_n * w_n) + b`
3.  **Aplica una Función de Activación:** La suma ponderada pasa a través de una **función de activación** `f()`. Esta función introduce no-linealidad en el modelo, lo cual es crucial para que la red pueda aprender patrones complejos. La salida de la neurona es `y = f(Suma)`.

![Perceptrón](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Perceptron_moj.png/440px-Perceptron_moj.png)

### Funciones de Activación Comunes

*   **Sigmoide:** Comprime cualquier valor real en el rango `(0, 1)`. Fue muy popular, pero puede sufrir del problema del "gradiente desvaneciente".
*   **Tanh (Tangente Hiperbólica):** Comprime los valores en el rango `(-1, 1)`. Es similar a la sigmoide pero centrada en cero.
*   **ReLU (Rectified Linear Unit):** Es la función más popular hoy en día. Su fórmula es `f(x) = max(0, x)`. Es muy simple: si la entrada es negativa, la salida es 0; si es positiva, la salida es la propia entrada. Es computacionalmente muy eficiente.

## 3. Arquitectura de una Red Neuronal (Multi-Layer Perceptron - MLP)

Una red neuronal se construye organizando las neuronas en capas:

*   **Capa de Entrada (Input Layer):** Recibe los datos brutos. El número de neuronas en esta capa es igual al número de características (features) de nuestro dataset.
*   **Capas Ocultas (Hidden Layers):** Son las capas intermedias entre la entrada y la salida. Aquí es donde ocurre la mayor parte del "aprendizaje". Una red puede tener una o muchas capas ocultas. Las redes con muchas capas ocultas se denominan "redes neuronales profundas" (Deep Learning).
*   **Capa de Salida (Output Layer):** Produce el resultado final. El número de neuronas y la función de activación en esta capa dependen del tipo de problema:
    *   **Regresión:** Típicamente una sola neurona con una función de activación lineal (o ninguna).
    *   **Clasificación Binaria:** Una sola neurona con una función de activación sigmoide.
    *   **Clasificación Multiclase:** Tantas neuronas como clases haya, con una función de activación **Softmax**, que convierte las salidas en una distribución de probabilidad.

Un **Multi-Layer Perceptron (MLP)** es una red neuronal con al menos una capa oculta.

## 4. ¿Cómo Aprende una Red Neuronal?

El proceso de "aprendizaje" consiste en encontrar los pesos y sesgos óptimos para que la red haga las predicciones más precisas posibles. Esto se logra a través de un proceso iterativo:

1.  **Inicialización:** Los pesos de la red se inicializan con valores aleatorios pequeños.
2.  **Propagación hacia Adelante (Forward Propagation):**
    *   Se toma una muestra (o un lote de muestras) de los datos de entrenamiento.
    *   Los datos pasan a través de la red, capa por capa, desde la entrada hasta la salida.
    *   La red genera una predicción.
3.  **Cálculo de la Pérdida (Loss Function):**
    *   Se compara la predicción de la red con el valor real (la etiqueta).
    *   Una **función de pérdida** (o función de coste) calcula qué tan "equivocada" está la predicción. Ejemplos: Error Cuadrático Medio para regresión, Entropía Cruzada para clasificación.
4.  **Propagación hacia Atrás (Backpropagation):**
    *   Este es el paso clave. El algoritmo calcula cómo contribuyó cada peso y sesgo de la red al error total. Lo hace calculando el gradiente (la derivada) de la función de pérdida con respecto a cada peso.
5.  **Actualización de Pesos (Optimización):**
    *   Un algoritmo de optimización, como el **Descenso de Gradiente (Gradient Descent)**, utiliza estos gradientes para ajustar ligeramente cada peso y sesgo en la dirección que reduce el error.
    *   La **tasa de aprendizaje (learning rate)** es un hiperparámetro que controla el tamaño de estos ajustes.

Estos cinco pasos se repiten muchas veces (durante muchas **épocas** o *epochs*) con todos los datos de entrenamiento, hasta que la red converge a un conjunto de pesos que minimiza la función de pérdida.

## 5. Sobreajuste (Overfitting) y Regularización

Las redes neuronales, al ser tan flexibles, tienen una alta tendencia al sobreajuste: pueden "memorizar" los datos de entrenamiento en lugar de aprender el patrón general.

**Técnicas de Regularización para Combatir el Sobreajuste:**

*   **Dropout:** Durante el entrenamiento, en cada iteración, se "apagan" o ignoran aleatoriamente un porcentaje de las neuronas de una capa. Esto fuerza a la red a aprender rutas redundantes y a no depender excesivamente de unas pocas neuronas.
*   **Regularización L1 y L2:** Se añade una penalización a la función de pérdida basada en la magnitud de los pesos. Esto anima a la red a mantener los pesos pequeños, lo que resulta en un modelo más simple y menos propenso al sobreajuste.
*   **Early Stopping:** Se monitorea el rendimiento del modelo en un conjunto de validación separado. Si el rendimiento en la validación deja de mejorar (o empieza a empeorar) durante un número determinado de épocas, se detiene el entrenamiento.

## 6. Tipos de Redes Neuronales (Más Allá del MLP)

*   **Redes Neuronales Convolucionales (CNNs):** Son el estándar de oro para tareas de visión por computadora (procesamiento de imágenes). Utilizan "filtros" convolucionales para detectar patrones espaciales como bordes, texturas y formas.
*   **Redes Neuronales Recurrentes (RNNs):** Diseñadas para trabajar con datos secuenciales, como series temporales o texto. Tienen "memoria" a través de conexiones recurrentes que les permiten mantener información de pasos anteriores.
