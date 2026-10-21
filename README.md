<div align="center">
  <h1>🍩 Clasificación de Personajes de Los Simpsons con CNNs 🍩</h1>
  <p><b>Evaluación Parcial N° 2 - Deep Learning (DLY0100)</b></p>
  <p><i>Duoc UC - 2do Semestre 2026</i></p>

  <!-- Badges -->
  <img src="https://img.shields.io/badge/Python-3.13-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/TensorFlow-2.21-orange?style=for-the-badge&logo=tensorflow&logoColor=white" alt="TensorFlow">
  <img src="https://img.shields.io/badge/Keras-API-red?style=for-the-badge&logo=keras&logoColor=white" alt="Keras">
  <img src="https://img.shields.io/badge/Accuracy-97.42%25-success?style=for-the-badge" alt="Accuracy">
</div>

<br>

## 📝 Descripción del Proyecto
Este repositorio contiene el desarrollo de una Red Neuronal Convolucional (CNN) implementada desde cero utilizando **TensorFlow y Keras**. El objetivo principal es clasificar imágenes de **18 personajes principales de la serie Los Simpsons**, superando el umbral mínimo exigido del 85% de *accuracy* en el set de prueba.

El proyecto incluye un análisis exhaustivo de los datos, preprocesamiento, técnicas avanzadas de regularización (Data Augmentation, Dropout, Batch Normalization) y un **Estudio de Ablación** para justificar empíricamente las decisiones de diseño de la arquitectura.

## 📂 Dataset
*   **Fuente:** [The Simpsons Characters Dataset (Kaggle)](https://www.kaggle.com/datasets/alexattia/the-simpsons-characters-dataset)
*   **Volumen:** ~20,933 imágenes en total.
*   **Nota técnica:** El archivo `.tar.gz` original proporcionado contenía solo 896 imágenes (insuficientes para entrenar una CNN desde cero sin sobreajuste severo). Por lo tanto, se optó por descargar el dataset oficial completo desde Kaggle para garantizar un entrenamiento robusto.
*   **Clases (18):** Homer, Bart, Lisa, Marge, Apu, Burns, Wiggum, entre otros.

## 🛠️ Tecnologías Utilizadas
*   **Lenguaje:** Python
*   **Deep Learning:** TensorFlow / Keras
*   **Procesamiento de Imágenes:** OpenCV (cv2)
*   **Análisis de Datos:** Scikit-Learn, NumPy, Pandas
*   **Visualización:** Matplotlib, Seaborn

## 🧠 Metodología y Decisiones Técnicas

1.  **Preprocesamiento:**
    *   Redimensionamiento de todas las imágenes a `64x64` píxeles para optimizar el cómputo.
    *   Normalización de píxeles dividiendo entre 255 (rango 0 a 1).
    *   División del set de entrenamiento en Train/Validation (80% / 20%).
2.  **Manejo del Desbalanceo:**
    *   Se analizó el dataset con un histograma, evidenciando que Homer tenía más de 2,000 imágenes y otros personajes menos de 400.
    *   Se implementó `class_weight` para penalizar más al modelo si se equivocaba en las clases minoritarias.
3.  **Arquitectura CNN:**
    *   3 bloques convolucionales (32, 64 y 128 filtros) con activación `ReLU`.
    *   Capas de `MaxPooling2D` para reducción de dimensionalidad.
    *   `BatchNormalization` para estabilizar el gradiente.
    *   `Dropout` (0.25 en convoluciones y 0.5 en capa densa) para prevenir el Overfitting.
4.  **Optimización:**
    *   Optimizador **Adam** (Learning Rate = 0.001).
    *   **Data Augmentation** (rotaciones, zooms, volteos) para simular imágenes reales y mejorar la generalización.
    *   Callbacks: `ReduceLROnPlateau` (para afinar el aprendizaje si se estanca) y `EarlyStopping`.

## 📊 Resultados y Estudio de Ablación
Se entrenaron tres modelos para comparar el impacto de las técnicas de regularización:

| Modelo | Regularización | Data Augmentation | Accuracy (Validación) | Accuracy (Test) |
| :--- | :--- | :--- | :--- | :--- |
| **Baseline** | ❌ No | ❌ No | ~75% (Estancado) | N/A |
| **Intermedio** | ✅ Sí (Dropout/BatchNorm) | ❌ No | ~85% | N/A |
| **Final** | ✅ Sí (Dropout/BatchNorm) | ✅ Sí | **~93%** | **97.42%** |

**Análisis:** El modelo Baseline sufrió un Overfitting severo (Train 99%, Val 75%). La inclusión de Data Augmentation en el Modelo Final fue el factor determinante que permitió a la red aprender características espaciales robustas en lugar de memorizar los datos.

## 🚀 ¿Cómo ejecutar este proyecto?

Para reproducir este cuaderno, sigue estos pasos:

1.  Clona este repositorio o abre el archivo `.ipynb` directamente en **Google Colab**.
2.  Asegúrate de tener activada la **GPU (T4)** en Colab: `Entorno de ejecución > Cambiar tipo de entorno > GPU`.
3.  **Configurar Token de Kaggle:**
    *   Ve a tu cuenta de Kaggle > `Account` > `Create New API Token`.
    *   Copia tu token (comienza con `KGAT_...`).
    *   En la **Celda 2** del notebook, reemplaza el texto `"INGRESE_SU_TOKEN_AQUI"` por tu token real.
4.  Ejecuta todas las celdas en orden (`Entorno de ejecución > Ejecutar todas`).

> **Advertencia de Seguridad:** El token de Kaggle en este repositorio ha sido removido/ocultado por motivos de seguridad. No subas tus credenciales a repositorios públicos.

## 👨‍💻 Autor
*   **David Santibáñez** - *Desarrollo del modelo, análisis y documentación.*

---
*Este proyecto fue desarrollado como parte de los requisitos de la asignatura Deep Learning en Duoc UC.*
