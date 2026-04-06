# 🧠 Clasificación de Imágenes con Deep Learning: Bart vs Homero

Este proyecto tiene como objetivo desarrollar y evaluar modelos de *deep learning* para la clasificación de imágenes de personajes de la serie *The Simpsons*, específicamente **Bart Simpson** y **Homero Simpson**.
El dataset puede encontrarse alojado en Kaggle en el siguiente enlace: https://www.kaggle.com/datasets/juniorbueno/neural-networks-homer-and-bart-classification
---

## 📌 Descripción del problema

Se aborda un problema de **clasificación binaria de imágenes**, donde el modelo debe predecir la clase de una imagen de entrada:

* **0 → Bart Simpson**
* **1 → Homero Simpson**

Este problema se enmarca dentro del área de **visión por computador**, utilizando redes neuronales convolucionales (CNN) como principal técnica de modelado.

---

## 🎯 Objetivos

* Desarrollar un modelo base de clasificación de imágenes.
* Implementar un enfoque iterativo para mejorar el desempeño del modelo.
* Evaluar el impacto de distintas técnicas de deep learning:

  * Data augmentation
  * Regularización
  * Transfer learning
* Comparar el desempeño de múltiples modelos bajo un mismo conjunto de métricas.

---

## 🗂️ Dataset

El dataset utilizado contiene **270 imágenes** distribuidas entre dos clases (Bart y Homero).

### Características:

* Imágenes RGB
* Variabilidad en resolución, iluminación y fondo
* Dataset balanceado (aproximadamente)

### Consideraciones:

Debido al tamaño reducido del dataset, se implementan estrategias como:

* Aumento de datos (*data augmentation*)
* Transfer learning
* Regularización

Fuente: Kaggle

---

## ⚙️ Metodología

El proyecto se desarrolla bajo un enfoque incremental:

### 🔹 Iteración 1: Modelo base

* CNN simple
* Preprocesamiento básico

### 🔹 Iteración 2: Mejoras

* Data augmentation
* Dropout
* Ajuste de hiperparámetros

### 🔹 Iteración 3: Modelos avanzados

* Transfer learning (VGG16 / ResNet)
* Fine-tuning

---

## 📏 Métricas de evaluación

Se utilizan métricas estándar de clasificación binaria:

* Accuracy
* Precision
* Recall
* F1-score
* Matriz de confusión

Estas métricas permiten comparar objetivamente el desempeño de los distintos modelos implementados.

---

## 📊 Resultados esperados

* Identificación del modelo con mejor desempeño
* Análisis del impacto de cada técnica aplicada
* Evaluación del comportamiento del modelo ante datos limitados

---

## 🧪 Tecnologías y librerías utilizadas

* Python
* TensorFlow / Keras
* NumPy
* Matplotlib
* Scikit-learn

---

## 📁 Estructura del proyecto

```
/data          # Dataset de imágenes
/notebooks     # Experimentos y pruebas
/src           # Código fuente
/models        # Modelos entrenados
/results       # Resultados y métricas
README.md
```

## 📚 Referencias

* LeCun, Y. et al. (1998). Gradient-based learning applied to document recognition.
* Krizhevsky, A. et al. (2012). ImageNet classification with deep convolutional neural networks.
* Simonyan, K. & Zisserman, A. (2014). Very Deep Convolutional Networks.
* He, K. et al. (2015). Deep Residual Learning (ResNet).

---

## 👨‍💻 Autor

Juan Manuel Vera Osorio
juan.verao@udea.edu.co
