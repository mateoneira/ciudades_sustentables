# Temas Avanzados - CNNs y Transfer Learning

## Parte 1: Redes Neuronales Convolucionales (CNNs)

### 1. ¿Por qué no usar un MLP para Imágenes?

En el tutorial anterior, usamos un Perceptrón Multicapa (MLP) para clasificar imágenes de 8x8 píxeles. Aplanamos la imagen en un vector de 64 características. Esto funciona para imágenes muy pequeñas, pero falla estrepitosamente con imágenes más grandes y complejas por varias razones:

*   **Pérdida de Información Espacial:** Al aplanar la imagen, perdemos la estructura 2D. La información sobre qué píxeles están cerca de otros se destruye.
*   **Explosión de Parámetros:** Una imagen de 224x224 píxeles (un tamaño común) tiene 50,176 píxeles. Si es a color (3 canales: R, G, B), son 150,528 características. Una sola neurona en la primera capa oculta tendría más de 150,000 pesos. Una capa con 1000 neuronas tendría 150 millones de pesos. Esto hace que el modelo sea computacionalmente carísimo y extremadamente propenso al sobreajuste.
*   **Falta de Invarianza:** Un MLP entrenado para reconocer un objeto en la esquina superior izquierda de una imagen no lo reconocerá si el mismo objeto aparece en la esquina inferior derecha.

Las **Redes Neuronales Convolucionales (CNNs)** fueron diseñadas específicamente para superar estos problemas.

### Los Bloques Fundamentales de una CNN

#### a) La Capa Convolucional (Convolutional Layer)

Esta es la capa principal de una CNN. En lugar de conectar cada neurona de entrada a cada neurona de la capa siguiente, utiliza **filtros** (también llamados **kernels**).

*   **Filtro/Kernel:** Un filtro es una pequeña matriz de pesos (e.g., 3x3 o 5x5). Este filtro se "desliza" o "convoluciona" sobre toda la imagen de entrada.
*   **Detección de Características:** Cada filtro está especializado en detectar una característica específica, como un borde vertical, un borde horizontal, una esquina, un color particular, etc.
*   **Mapa de Características (Feature Map):** En cada posición, el filtro realiza una operación de producto punto con la porción de la imagen que está cubriendo. El resultado es un único número. Al deslizar el filtro por toda la imagen, se genera una nueva matriz 2D llamada "mapa de características", que indica dónde (en qué zonas de la imagen) se detectó la característica que el filtro busca.

Una capa convolucional aplica múltiples filtros a la imagen de entrada, generando así múltiples mapas de características.

**Ventajas Clave:**
*   **Preservación Espacial:** Mantiene la estructura 2D de la imagen.
*   **Compartición de Parámetros (Parameter Sharing):** El mismo filtro (con los mismos pesos) se reutiliza en toda la imagen. Esto reduce drásticamente el número de parámetros a aprender.
*   **Invarianza a la Traslación:** Como el mismo filtro se aplica en todas partes, la red puede detectar una característica sin importar en qué parte de la imagen aparezca.

#### La Capa de Agrupación (Pooling Layer)

Después de una capa convolucional, es común aplicar una capa de agrupación. Su objetivo es reducir la dimensionalidad espacial (el ancho y alto) de los mapas de características.

*   **Operación:** La forma más común es el **Max Pooling**. Se divide el mapa de características en una cuadrícula (e.g., de 2x2) y, para cada celda de la cuadrícula, se toma solo el valor máximo.
*   **Beneficios:**
    *   Reduce el número de parámetros y la carga computacional en las capas posteriores.
    *   Proporciona una forma de invarianza a pequeñas traslaciones (si una característica se mueve un poco dentro de la ventana de pooling, la salida del max pooling probablemente no cambiará).
    *   Hace que la red se enfoque en la presencia de características en lugar de su ubicación exacta.

#### La Capa Totalmente Conectada (Fully Connected Layer)

Después de varias capas convolucionales y de pooling, la arquitectura de la CNN suele terminar con una o más capas totalmente conectadas, como las que vimos en un MLP.

*   **Aplanamiento (Flatten):** Los mapas de características 2D que salen de la última capa de pooling se aplanan en un único vector largo.
*   **Clasificación:** Este vector se pasa a una o más capas totalmente conectadas que realizan la tarea final de clasificación (o regresión), culminando en una capa de salida con una función de activación Softmax (para clasificación).

## Parte 2: Aprendizaje por Transferencia (Transfer Learning)

### 1. El Desafío del Entrenamiento

Entrenar una CNN profunda desde cero en un conjunto de datos grande (como ImageNet, con más de 14 millones de imágenes y 1000 clases) requiere una enorme cantidad de datos y una potencia computacional masiva (semanas o meses en múltiples GPUs).

### 2. La Idea Clave

Afortunadamente, no tenemos que hacerlo. Podemos aprovechar el trabajo de otros. La idea del **aprendizaje por transferencia** es tomar una red neuronal que ya ha sido entrenada en una tarea a gran escala (como la clasificación en ImageNet) y adaptarla para nuestra propia tarea, que generalmente involucra un conjunto de datos mucho más pequeño.

**¿Por qué funciona?** Las primeras capas de una CNN entrenada en ImageNet aprenden a detectar características muy generales que son útiles para casi cualquier tarea de visión: bordes, colores, texturas, gradientes, etc. Las capas intermedias aprenden a combinar estas características para formar partes de objetos (ojos, ruedas, hojas). Las últimas capas aprenden a reconocer objetos completos.

Podemos reutilizar el "conocimiento" de las capas iniciales e intermedias para nuestra propia tarea.

### 3. Estrategias de Transfer Learning

#### Extracción de Características (Feature Extraction)

Esta es la estrategia más común y sencilla.
1.  **Cargar un Modelo Pre-entrenado:** Se carga una arquitectura de CNN conocida (como VGG16, ResNet50, MobileNetV2) con los pesos ya entrenados en ImageNet.
2.  **Congelar la Base Convolucional:** Se "congelan" todas las capas convolucionales del modelo pre-entrenado. Esto significa que sus pesos no se actualizarán durante nuestro entrenamiento.
3.  **Añadir una Nueva Cabeza Clasificadora:** Se elimina la capa de salida original del modelo (que estaba diseñada para las 1000 clases de ImageNet) y se reemplaza por nuestras propias capas totalmente conectadas y una nueva capa de salida adaptada a nuestro número de clases.
4.  **Entrenar solo la Nueva Cabeza:** Se entrena el modelo en nuestro dataset. Como la base convolucional está congelada, solo se entrenarán los pesos de la nueva cabeza clasificadora que acabamos de añadir.

Esto es rápido y funciona muy bien, especialmente si nuestro dataset es pequeño.

#### Ajuste Fino (Fine-Tuning)

Esta técnica es una extensión de la anterior y puede dar un extra de rendimiento.
1.  Se siguen los mismos pasos que en la extracción de características (cargar, congelar, añadir cabeza, entrenar la cabeza).
2.  **Descongelar las Últimas Capas:** Después de que la nueva cabeza clasificadora se ha entrenado un poco, se "descongelan" las últimas capas de la base convolucional pre-entrenada.
3.  **Continuar el Entrenamiento:** Se sigue entrenando el modelo, pero ahora con una **tasa de aprendizaje muy baja**. Esto permite que los pesos de las capas descongeladas se ajusten sutilmente para adaptarse mejor a las características específicas de nuestro nuevo dataset, sin destruir el conocimiento general que ya habían aprendido.

El ajuste fino es más delicado y requiere más tiempo, pero a menudo conduce a mejores resultados.
