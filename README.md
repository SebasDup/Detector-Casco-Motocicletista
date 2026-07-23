# 🏍️ Modelo Detector de Casco para Motociclistas (CNN)

## 📝 Descripción del Proyecto
Este proyecto consiste en un modelo de Inteligencia Artificial basado en Redes Neuronales Convolucionales (CNN) diseñado para procesar imágenes y detectar automáticamente si un motociclista lleva puesto el casco o no. 

El objetivo principal es ofrecer una solución tecnológica a la problemática de seguridad vial, reduciendo la dependencia de intervenciones humanas o la revisión manual de cámaras de vigilancia para identificar infracciones que pueden resultar en lesiones graves o fatales.

## 🛠️ Tecnologías y Librerías Utilizadas
* **Lenguaje:** Python.
* **Framework de Deep Learning:** Keras y TensorFlow (uso de `Sequential`, `Dense`, `Convolution2D`).
* **Visión por Computadora:** OpenCV (`cv2`) para el procesamiento de las imágenes.
* **Interfaz Gráfica (UI):** Gradio, utilizado para desplegar el modelo en un entorno web interactivo (`http://...gradio.live`) donde el usuario puede subir una foto y ver las probabilidades.

## 🧠 Arquitectura del Modelo Convolucional
El modelo fue construido de manera secuencial y configurado con los siguientes hiperparámetros para optimizar la extracción de características:

* **Capa de Entrada:** Imágenes redimensionadas a $150 \times 150$ píxeles con 3 canales de color (RGB).
* **Capas de Convolución:** 
  * Primera capa con 32 filtros (kernel de $3 \times 3$) y activación ReLU.
  * Segunda capa con 64 filtros (kernel de $3 \times 3$) y activación ReLU.
* **Submuestreo:** Aplicación de `MaxPooling2D` (con tamaño de pool de $3 \times 3$) tras cada convolución para reducir la dimensionalidad.
* **Aplanamiento (Flatten):** Transformación de las matrices resultantes en un vector unidimensional.
* **Red Neuronal Multicapa (MLP):** 
  * Primera capa oculta densa de 100 neuronas (activación ReLU).
  * Segunda capa oculta densa de 50 neuronas (activación ReLU).
* **Regularización:** Capa de `Dropout` configurada al 0.3 (30%) para apagar neuronas aleatoriamente y prevenir el sobreajuste (overfitting).
* **Capa de Salida:** 2 clases de clasificación mediante la función de activación `softmax`.

## 📊 Preprocesamiento y Entrenamiento (Data Augmentation)
Para mejorar la robustez del modelo y compensar la cantidad de datos, se aplicaron técnicas de generación de datos sintéticos (Data Augmentation) utilizando `ImageDataGenerator`. 

* **Transformaciones aplicadas:** Reescalado ($1/200$), rango de zoom ($0.30$) y volteo horizontal (horizontal flip).
* **Distribución del Dataset:** El modelo fue entrenado con un total de 1,924 imágenes para entrenamiento, 480 para validación y 10 para pruebas.
* **Compilación:** Se utilizó la función de pérdida `categorical_crossentropy`, el optimizador `adam` y métricas de precisión (`acc`) y error cuadrático medio (`mse`) durante 30 épocas en lotes (batch size) de 16.

## 🚀 Cómo probar el modelo
1. Clona este repositorio: `git clone https://github.com/tu-usuario/detector-cascos-cnn.git`
2. Instala las dependencias necesarias: `pip install tensorflow keras opencv-python gradio`
3. Ejecuta el script principal para levantar la interfaz local.
4. Abre la dirección generada por Gradio en tu navegador, sube una foto de un motociclista y observa el análisis de confianza por clase (Sí tiene casco / No tiene casco).

## ☁️ Cómo probar el modelo en la nube (Google Colab)

Si deseas probar el modelo sin necesidad de configurar un entorno local de Python o instalar librerías pesadas, puedes ejecutar este proyecto directamente en la nube utilizando Google Colab y Google Drive. Sigue estos pasos:

### 1. Preparar el entorno en Google Drive
1. Descarga el código y los archivos de este repositorio.
2. Sube la carpeta completa a la raíz de tu Google Drive. 
3. **⚠️ Importante:** Asegúrate de que la carpeta principal se llame exactamente `Deteccion_de_Casco` y que esté en la vista principal de tu Drive (`MyDrive`). Si le cambias el nombre o la guardas dentro de otra subcarpeta, el código no encontrará las rutas de las imágenes ni del modelo.

### 2. Ejecutar el código en Google Colab
1. Ingresa a [Google Colab](https://colab.research.google.com/).
2. En la ventana emergente, selecciona la pestaña **Subir** (Upload) y carga el archivo `modelo_deteccion_casco.ipynb` que viene en el proyecto.
3. Ejecuta la primera celda del código haciendo clic en el botón de "Play" (▶️). Esta celda contiene el comando `drive.mount('/content/drive')`. 
4. Colab te pedirá autorización para acceder a tus archivos de Drive. Haz clic en **Permitir** (esto es estrictamente necesario para que el código pueda leer los pesos del modelo y el set de imágenes).

### 3. Lanzar la Interfaz Gráfica (Gradio)
1. Una vez conectado el Drive, ejecuta el resto de las celdas de código una por una hacia abajo.
2. Al ejecutar la última celda (la de configuración de Gradio), el sistema procesará la interfaz y generará una URL pública en la terminal (con un formato similar a `https://....gradio.live`).
3. Haz clic en ese enlace para abrir la aplicación web. ¡Listo! Ya puedes cargar tus propias imágenes y poner a prueba el detector de cascos.

## 📸 Demostración
<img width="1896" height="916" alt="Screenshot 2026-07-22 205641" src="https://github.com/user-attachments/assets/98b53bc0-12c1-4215-9a5f-6f2d6f67bb19" />
<img width="1896" height="916" alt="Screenshot 2026-07-22 205404" src="https://github.com/user-attachments/assets/447d3ba8-4e0e-485a-8028-8d6ed995aaaf" />
<img width="1890" height="905" alt="Screenshot 2026-07-22 205439" src="https://github.com/user-attachments/assets/49b51f1a-870b-448f-ba48-f6980edf319c" />
<img width="1891" height="896" alt="Screenshot 2026-07-22 205520" src="https://github.com/user-attachments/assets/20ce090f-3ba6-4500-b3f3-324f5bbec0a8" />
