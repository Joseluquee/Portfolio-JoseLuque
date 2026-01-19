\# Denoising Autoencoder - Fashion MNIST



\## Descripción

Este proyecto implementa un \*\*Denoising Autoencoder (DAE)\*\* usando \*\*PyTorch\*\* sobre el dataset \*\*Fashion MNIST\*\*.  

El objetivo es entrenar un modelo que \*\*elimine ruido de las imágenes\*\* y reconstruya versiones limpias a partir de imágenes ruidosas.



El proyecto demuestra:  

\- Implementación de un autoencoder con \*\*espacio latente reducido\*\*.  

\- Aplicación de \*\*ruido gaussiano\*\* a las imágenes de entrada.  

\- Uso de \*\*early stopping\*\* para evitar sobreajuste.  

\- Visualización de la reconstrucción de imágenes y del \*\*espacio latente\*\*.



---



\## Dataset

Se utilizó el dataset \*\*Fashion MNIST\*\*, que contiene:  

\- 60,000 imágenes de entrenamiento (28x28, escala de grises)  

\- 10,000 imágenes de test  

\- 10 clases: `T-shirt/top, Trouser, Pullover, Dress, Coat, Sandal, Shirt, Sneaker, Bag, Ankle boot`  



El dataset se dividió en:  

\- 50,000 ejemplos para entrenamiento  

\- 10,000 ejemplos para validación  



Se añadió \*\*ruido gaussiano\*\* con media `0` y desviación estándar `0.2` a las imágenes para el entrenamiento del autoencoder.



---



\## Arquitectura del Modelo

El \*\*Denoising Autoencoder\*\* se compone de:  



\*\*Encoder:\*\*  

\- Flatten de la imagen 28x28  

\- Linear (784 → 128) + LeakyReLU  

\- Linear (128 → 64) + LeakyReLU  

\- Linear (64 → 8) → espacio latente de dimensión 8  



\*\*Decoder:\*\*  

\- Linear (8 → 64) + LeakyReLU  

\- Linear (64 → 128) + LeakyReLU  

\- Linear (128 → 784) + Sigmoid → reconstrucción de la imagen  



Se entrenó usando:  

\- \*\*Loss:\*\* L1Loss (mean absolute error)  

\- \*\*Optimizador:\*\* Adam con learning rate `1e-3`  

\- \*\*Early stopping:\*\* paciencia 25, delta 1e-3  

\- \*\*Épocas máximas:\*\* 200  

\- \*\*Batch size:\*\* 4096



---



\## Metodología

1\. Se añade ruido gaussiano a las imágenes de entrenamiento y test.  

2\. Se entrena el autoencoder para reconstruir imágenes limpias a partir de imágenes ruidosas.  

3\. Se monitoriza la pérdida en entrenamiento y validación.  

4\. Se aplica early stopping para evitar sobreajuste.  

5\. Se evalúa el \*\*error medio absoluto\*\* en el conjunto de test.  

6\. Se visualizan ejemplos de:  

&nbsp;  - Imagen limpia  

&nbsp;  - Imagen con ruido  

&nbsp;  - Imagen reconstruida por el autoencoder  

7\. Se proyecta el espacio latente de 8 dimensiones en pares para visualizar cómo las imágenes se distribuyen según su clase.



---



\## Resultados

\- \*\*Error medio absoluto en test:\*\* 0.06857  

\- El modelo logra \*\*reconstruir imágenes ruidosas\*\* de manera efectiva, preservando detalles de las clases.  

\- Las visualizaciones del espacio latente muestran \*\*agrupamientos por clase\*\*, lo que indica que el modelo aprende representaciones significativas.



---



\## Lecciones Aprendidas

\- Comprensión de la \*\*arquitectura de autoencoders\*\* y su entrenamiento.  

\- Cómo manejar \*\*datasets con ruido\*\* y entrenar modelos robustos.  

\- Implementación de \*\*early stopping\*\* y monitorización de pérdidas de entrenamiento y validación.  

\- Análisis del \*\*espacio latente\*\* como representación de las clases de datos.  

\- Preparación para trabajar con modelos generativos más complejos, como \*\*Variational Autoencoders\*\*.



