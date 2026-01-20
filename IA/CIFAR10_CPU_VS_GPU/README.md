# CIFAR-10 CPU vs GPU - Clasificación de Imágenes con PyTorch

## Descripción

Este proyecto compara el entrenamiento de un modelo de red neuronal para clasificación de imágenes **CIFAR-10** usando **CPU y GPU**.  

El objetivo es analizar **diferencias de velocidad y rendimiento** entre ambos dispositivos mientras se entrenan modelos equivalentes.

El proyecto fue desarrollado como práctica académica utilizando **PyTorch**, mostrando:  

- Entrenamiento de un modelo secuencial simple (MLP).  
- Uso de early stopping para evitar sobreajuste.  
- Comparación de métricas de validación y tiempo de entrenamiento.  
- Visualización de matrices de confusión y evolución de loss y accuracy.

---

## Dataset

Se utilizó el dataset **CIFAR-10**, que contiene:  

- 50,000 imágenes de entrenamiento  
- 10,000 imágenes de test  
- 10 clases: `airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck`  

Se dividió en:  

- 45,000 ejemplos para entrenamiento  
- 5,000 ejemplos para validación  
- 10,000 ejemplos para test  

Las imágenes fueron normalizadas con la media y desviación estándar del dataset.

---

## Arquitectura del Modelo

El modelo utilizado es un **MLP simple**, compuesto por:  

- Flatten de las imágenes 32x32x3  
- Linear (3072 → 128) + LeakyReLU  
- Linear (128 → 64) + LeakyReLU  
- Linear (64 → 10) + LogSoftmax  

Se entrenó usando **NLLLoss** y el optimizador **Adam** con learning rate `5e-5`.  

Se implementó **early stopping** con paciencia de 15 épocas y delta de 1e-3.

---

## Metodología

1. Se entrenó el modelo primero en CPU y luego en GPU.  
2. Se registraron métricas durante el entrenamiento:  
   - Loss de entrenamiento por época  
   - Loss de validación cada `validation_freq` épocas  
   - Accuracy de validación cada `validation_freq` épocas  
3. Se calcularon tiempos promedio por época en ambos dispositivos.  
4. Se generaron gráficas y matrices de confusión para evaluar el desempeño.

---

## Resultados

### Comparativa de tiempo por época

> La GPU mostró un **2225.15% más rápida** que la CPU en promedio por época.

### Accuracy

- Valor de accuracy final (validación): 0.5192  

---

## Lecciones Aprendidas

- Comprensión de diferencias de velocidad entre CPU y GPU en entrenamiento de redes neuronales.  
- Implementación de early stopping para evitar sobreajuste.  
- Visualización de métricas y resultados de manera clara y profesional.  
- Preparación para manejar datasets y entrenar modelos prácticos de IA.

---

