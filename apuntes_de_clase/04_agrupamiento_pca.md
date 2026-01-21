# Modelos de Agrupamiento y Reducción de Dimensionalidad

**Duración:** 4 horas (2h Lectura, 2h Tutorial)

---

## Objetivos de la Sesión

*   Comprender la diferencia entre aprendizaje supervisado y **no supervisado**.
*   Aprender la intuición y aplicación de dos algoritmos de clustering (agrupamiento) clave:
    1.  **K-Means:** Un método basado en centroides para encontrar grupos esféricos.
    2.  **DBSCAN:** Un método basado en densidad, capaz de encontrar grupos de formas arbitrarias e identificar ruido.
*   Entender el propósito de la **reducción de dimensionalidad**.
*   Introducir el **Análisis de Componentes Principales (PCA)** como la técnica más popular para reducir dimensiones.
*   **Meta Práctica:** Aplicar K-Means y DBSCAN para segmentar datos y usar PCA para visualizar datos de alta dimensionalidad.

---

## 1. Lectura: Descubriendo Patrones Ocultos (2 horas)

### 1.1 Aprendizaje No Supervisado

Hasta ahora, todos nuestros modelos han sido **supervisados**: teníamos una variable objetivo `y` (ej. `precio`, `alto_trafico_peatonal`) que queríamos predecir a partir de las características `X`.

En el **aprendizaje no supervisado**, no tenemos una variable objetivo. Solo tenemos las características `X`, y el objetivo es descubrir patrones, estructuras o grupos inherentes en los propios datos.

*   **Clustering (Agrupamiento):** La tarea de agrupar un conjunto de objetos de tal manera que los objetos en el mismo grupo (llamado **clúster**) sean más similares entre sí que con los de otros grupos.
    *   *Aplicación urbana:* Segmentar barrios de una ciudad en categorías (ej. "residencial de baja densidad", "comercial céntrico", "industrial") basándose en sus características.

*   **Reducción de Dimensionalidad:** La tarea de reducir el número de variables de entrada (características) en un conjunto de datos, conservando la mayor cantidad de información relevante posible.
    *   *Aplicación urbana:* Combinar 10 variables diferentes sobre la calidad del aire en 2 o 3 "índices de contaminación" principales.

### 1.2 Algoritmos de Clustering

#### K-Means
*   **La Idea Central:** Encontrar `k` centros de clúster (llamados **centroides**) y asignar cada punto de datos al centroide más cercano.
*   **¿Cómo funciona?**
    1.  **Elegir `k`:** Se elige de antemano el número de clústeres que se quieren encontrar.
    2.  **Inicialización:** Se colocan `k` centroides en posiciones aleatorias.
    3.  **Asignación:** Cada punto de datos se asigna al clúster del centroide más cercano (generalmente usando distancia euclidiana).
    4.  **Actualización:** La posición de cada centroide se recalcula como la media de todos los puntos asignados a su clúster.
    5.  **Repetición:** Los pasos 3 y 4 se repiten hasta que los centroides dejan de moverse significativamente.
*   **El gran desafío:** ¿Cómo elegir `k`? El **Método del Codo (Elbow Method)** es una heurística popular. Se ejecuta K-Means para diferentes valores de `k` y se grafica la inercia (suma de las distancias al cuadrado de cada punto a su centroide). Se busca el "codo" en el gráfico, el punto donde la inercia deja de disminuir drásticamente.
*   **Limitaciones:**
    *   Asume que los clústeres son esféricos y de tamaño similar.
    *   Es sensible a la inicialización aleatoria de los centroides.
    *   Requiere que las variables estén escaladas.

#### DBSCAN (Density-Based Spatial Clustering of Applications with Noise)
*   **La Idea Central:** Un clúster es una región densa de puntos, separada de otras regiones densas por áreas de baja densidad. Los puntos que no pertenecen a ninguna región densa se consideran **ruido (outliers)**.
*   **¿Cómo funciona?**
    *   Define un clúster basándose en dos parámetros:
        *   `eps` (épsilon): Un radio de distancia. ¿Qué tan lejos buscamos para encontrar vecinos?
        *   `min_samples`: El número mínimo de puntos que deben estar dentro del radio `eps` de un punto para que se considere un "punto central" (core point).
    *   El algoritmo expande los clústeres a partir de los puntos centrales.
*   **Ventajas:**
    *   **No necesita especificar el número de clústeres** de antemano.
    *   Puede encontrar clústeres de formas arbitrarias (no solo esféricos).
    *   **Identifica y etiqueta los outliers** de forma robusta.
*   **Desventajas:**
    *   Puede tener dificultades con clústeres de densidades muy diferentes.
    *   La elección de `eps` y `min_samples` puede no ser trivial.

### 1.3 Reducción de Dimensionalidad: PCA

*   **La "Maldición de la Dimensionalidad":** Cuando tenemos demasiadas características (alta dimensionalidad), los datos se vuelven muy dispersos, los cálculos se vuelven costosos y es más difícil encontrar patrones significativos.
*   **Análisis de Componentes Principales (PCA):** Es una técnica para transformar un conjunto de variables posiblemente correlacionadas en un nuevo conjunto de variables no correlacionadas llamadas **componentes principales**.
*   **La Idea Central:** PCA encuentra las "direcciones" en los datos donde hay más **varianza** (información).
    *   El **Primer Componente Principal (PC1)** es la dirección que captura la mayor cantidad de varianza en los datos.
    *   El **Segundo Componente Principal (PC2)** es la siguiente dirección, ortogonal (perpendicular) a la primera, que captura la mayor cantidad de la varianza restante.
    *   Y así sucesivamente...
*   **¿Cómo se usa?**
    1.  Se escalan los datos (PCA es muy sensible a la escala).
    2.  Se aplica PCA y se decide cuántos componentes principales conservar (ej. los que expliquen el 95% de la varianza total).
    3.  Se transforman los datos originales a este nuevo espacio de menor dimensión.
*   **Aplicación Principal:** **Visualización**. Es imposible visualizar datos en 10 dimensiones. Pero podemos usar PCA para reducirlos a 2 o 3 componentes principales y crear un gráfico de dispersión para ver la estructura de los datos (como los clústeres que hemos encontrado).
