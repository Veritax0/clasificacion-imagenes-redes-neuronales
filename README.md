# 🧠 Clasificación de Imágenes con Deep Learning: Bart vs Homero

Este proyecto tiene como objetivo desarrollar y evaluar modelos de *deep learning* para la clasificación de imágenes de personajes de la serie *The Simpsons*, específicamente **Bart Simpson** y **Homero Simpson**.

El dataset puede encontrarse alojado en Kaggle en el siguiente enlace:
🔗 [Homer & Bart Classification — Kaggle](https://www.kaggle.com/datasets/juniorbueno/neural-networks-homer-and-bart-classification)

## 🎬 Video de presentación

▶️ **[Enlace al video en YouTube](https://youtu.be/txmMNbnSpDE)**
---

## 📌 Descripción del problema

Se aborda un problema de **clasificación binaria de imágenes**, donde el modelo debe predecir la clase de una imagen de entrada:

* **0 → Bart Simpson**
* **1 → Homero Simpson**

El problema se formula como una función **f(x) → y**, donde `x` es una imagen RGB e `y` es una etiqueta binaria. Se enmarca dentro del área de **visión por computador**, utilizando redes neuronales convolucionales (CNN) y técnicas de transfer learning como principal estrategia de modelado.

---

## 🎯 Objetivos

* Desarrollar un modelo base (baseline) de clasificación de imágenes entrenado desde cero.
* Implementar un enfoque iterativo para mejorar el desempeño del modelo.
* Evaluar el impacto de distintas técnicas de deep learning:
  * Data augmentation geométrico
  * Regularización (Dropout, L2)
  * Transfer learning con fine-tuning (MobileNetV2)
  * Interpretabilidad visual (Grad-CAM)
* Comparar el desempeño de los modelos bajo un mismo conjunto de métricas.

---

## 🗂️ Dataset

El dataset utilizado contiene aproximadamente **270 imágenes BMP** distribuidas entre dos clases (Bart y Homero), con un peso total de 132 MB.

### Características

* Imágenes RGB en formato BMP, almacenadas en carpeta plana sin subdirectorios
* La etiqueta de clase se extrae del nombre del archivo (p. ej. `bart_001.bmp`, `homer_042.bmp`)
* Variabilidad en resolución, iluminación y fondo
* Dataset aproximadamente balanceado entre clases

### División del dataset

| Conjunto      | Proporción | Imágenes aprox. |
|---------------|-----------|-----------------|
| Entrenamiento | 70 %      | ~190            |
| Validación    | 15 %      | ~40             |
| Test          | 15 %      | ~40             |

> La división se realiza de forma **estratificada** para mantener la proporción de clases en cada partición.

### Obtención de los datos

Los notebooks descargan el dataset automáticamente mediante la API de Kaggle. Para ejecutarlos es necesario disponer de un archivo `kaggle.json` con las credenciales de usuario, obtenible desde:

> kaggle.com → Settings → API → **Create New Token**

En Google Colab basta con subir ese archivo cuando el notebook lo solicite. El código verifica si el directorio ya existe antes de descargar, haciendo el proceso idempotente.

---

## 🗒️ Notebooks

La solución se organiza en **dos notebooks numerados** directamente ejecutables en Google Colab.

| Notebook | Descripción |
|----------|-------------|
| `01_baseline_cnn.ipynb` | CNN entrenada desde cero. Establece la referencia mínima (baseline) para medir el impacto de las mejoras posteriores. |
| `02_mejoras_Data_Augmentation_Transfer_Learning.ipynb` | Mejoras sobre el baseline: data augmentation ampliado, Transfer Learning con MobileNetV2 en dos fases y análisis Grad-CAM. |

---

## ⚙️ Metodología

El proyecto se desarrolla bajo un enfoque incremental con tres iteraciones principales:

### 🔹 Iteración 1 — CNN baseline (`notebook 01`)

* Arquitectura CNN con tres bloques Conv2D → BatchNorm → ReLU → MaxPooling
* Augmentation ligero: flip horizontal, rotación ±10 %, zoom ±10 %
* Optimizador Adam (lr = 1e-3), batch size 4, hasta 30 épocas con EarlyStopping
* **Resultado:** Accuracy en test **63.41 %**

### 🔹 Iteración 2 — Transfer Learning Fase 1 (`notebook 02`)

* Backbone **MobileNetV2** preentrenado en ImageNet, completamente congelado
* Nueva cabeza clasificadora: GlobalAvgPooling2D → Dense(128, ReLU) + L2 → Dropout(0.4) → Dense(2, Softmax)
* Augmentation ampliado: flip H+V, rotación ±15 %, zoom ±15 %, traslación ±10 %
* lr = 1e-3, máximo 15 épocas

### 🔹 Iteración 3 — Fine-tuning parcial Fase 2 (`notebook 02`)

* Se descongelan las **últimas 54 capas** del backbone (de 154 totales)
* lr reducido a 1e-4 para preservar los features genéricos de las capas inferiores
* Callbacks: EarlyStopping, ReduceLROnPlateau, ModelCheckpoint
* **Resultado:** Accuracy en test **90.24 %**

---

## 📏 Métricas de evaluación

| Métrica | Descripción |
|---------|-------------|
| Accuracy | Proporción de predicciones correctas sobre el total |
| Precision | De las predicciones positivas, cuántas son correctas |
| Recall | De los positivos reales, cuántos se detectan |
| F1-score | Media armónica de precision y recall |
| Matriz de confusión | Distribución detallada de aciertos y errores por clase |
| AUC-ROC *(solo notebook 02)* | Capacidad discriminativa independiente del umbral |

---

## 📊 Resultados

| Métrica   | CNN Baseline | MobileNetV2 TL | Mejora      |
|-----------|:------------:|:--------------:|:-----------:|
| Accuracy  | 63.41 %      | **90.24 %**    | +26.83 pp   |
| Precision | 63.76 %      | **90.30 %**    | +26.54 pp   |
| Recall    | 63.41 %      | **90.24 %**    | +26.83 pp   |
| F1-score  | 0.6355       | **0.9030**     | +0.2675     |

El análisis **Grad-CAM** confirma que el modelo focaliza su atención en las características visuales propias de cada personaje (forma de la cabeza, ropa, rasgos faciales) y no en artefactos del fondo.

---

## 🎬 Video de presentación

▶️ **[Enlace al video en YouTube](https://youtu.be/txmMNbnSpDE)**


---

## 🧪 Tecnologías y librerías utilizadas

* Python 3
* TensorFlow / Keras
* NumPy
* Matplotlib
* Scikit-learn
* Kaggle API

---

## 📁 Estructura del proyecto

```
/
├── notebooks/
│   ├── 01_baseline_cnn.ipynb                                # CNN baseline entrenada desde cero
│   └── 02_mejoras_Data_Augmentation_Transfer_Learning.ipynb # Transfer Learning con MobileNetV2
├── INFORME_PROYECTO.PDF                                     # Informe ejecutivo final
├── ENTREGA1.PDF                                             # Informe primera entrega
└── README.md
```

---

## 📚 Referencias

* LeCun, Y. et al. (1998). Gradient-based learning applied to document recognition. *Proceedings of the IEEE*, 86(11), 2278–2324.
* Krizhevsky, A. et al. (2012). ImageNet classification with deep convolutional neural networks. *NeurIPS*.
* Sandler, M. et al. (2018). MobileNetV2: Inverted residuals and linear bottlenecks. *CVPR*.
* Selvaraju, R. R. et al. (2017). Grad-CAM: Visual explanations from deep networks via gradient-based localization. *ICCV*.
* He, K. et al. (2016). Deep residual learning for image recognition. *CVPR*.

---

## 👨‍💻 Autor

**Juan Manuel Vera Osorio**
juan.verao@udea.edu.co
