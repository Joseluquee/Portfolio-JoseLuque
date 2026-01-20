# Variational Autoencoder (VAE) - Fashion MNIST

## Descripción

Este proyecto implementa un **Variational Autoencoder (VAE)** para el dataset **Fashion MNIST**, con el objetivo de aprender una representación latente de las imágenes y generar nuevas muestras.

Se estudia la **reconstrucción de imágenes**, la **distribución en el espacio latente** y la **interpolación entre clases**.

El proyecto está desarrollado en **PyTorch** y utiliza GPU si está disponible.

---

## Dataset

Se utilizó **Fashion MNIST**, que contiene:

- 60,000 imágenes de entrenamiento
- 10,000 imágenes de test
- 10 clases: `T-shirt/top, Trouser, Pullover, Dress, Coat, Sandal, Shirt, Sneaker, Bag, Ankle boot`

Se dividió en:

- 50,000 ejemplos para entrenamiento
- 10,000 ejemplos para validación

Las imágenes se normalizan automáticamente con `ToTensor()` para tener valores en [0,1].

---

## Arquitectura del Modelo

El **VAE** se compone de:

### Encoder

- Flatten de las imágenes 28x28
- Linear 784 → 128 + LeakyReLU
- Linear 128 → 64 + LeakyReLU
- Dos capas lineales separadas para **mu** y **logvar**, cada una de tamaño 8 (dimensión latente)

### Reparametrización

- `z = mu + sigma * epsilon` con `epsilon ~ N(0,1)`

### Decoder

- Linear 8 → 64 + LeakyReLU
- Linear 64 → 128 + LeakyReLU
- Linear 128 → 784 + Sigmoid
- Reshape a 1x28x28

### Función de pérdida

- Reconstrucción: L1Loss media por píxel
- Regularización KL: `KL(N(mu, sigma^2) || N(0,1))`
- Pérdida total: `L = L_r + alpha * KL`, con `alpha = 1e-3`

---

## Metodología

1. Se movieron los datasets a GPU para acelerar el entrenamiento.
2. Entrenamiento del VAE durante 200 épocas con early stopping (paciencia = 25, delta = 1e-3).
3. Se registraron:
   - Loss de entrenamiento por época
   - Loss de validación cada 5 épocas
4. Se calculó la **pérdida total de test** (reconstrucción + KL).
5. Visualización:
   - Train vs validation loss
   - Proyecciones del espacio latente (pares de dimensiones)
   - Interpolación entre prototipos de diferentes clases

---

## Resultados

- **Test loss (recon + alpha * KL):** 0.08380
- El modelo logra **reconstruir imágenes de Fashion MNIST** de manera efectiva.
- Las visualizaciones del espacio latente muestran **agrupamientos por clase**, indicando que el VAE aprende representaciones significativas.
- Las **interpolaciones entre prototipos de clases** generan transiciones suaves, demostrando un **espacio latente continuo y coherente**.

---

## Lecciones Aprendidas

- Implementación de un modelo generativo avanzado (VAE).
- Comprensión de la pérdida KL y su impacto en el entrenamiento.
- Visualización y análisis de espacios latentes para modelos generativos.
- Capacidad de interpolación y generación de imágenes nuevas a partir del espacio latente.
