# AgroTech – Detección y clasificación de enfermedades en hojas de tomate

## Descripción del proyecto

Este proyecto fue desarrollado para la asignatura Seminario de Investigación de la Universidad del Quindío.

Su objetivo es implementar un sistema de visión artificial capaz de detectar hojas de tomate en fotografías tomadas en un cultivo, separarlas del fondo y clasificarlas según sus características visuales para identificar posibles enfermedades.

El sistema integra tres modelos de inteligencia artificial: YOLOv8 para la detección de hojas, MobileSAM para la segmentación y Vision Transformer (ViT V4) para la clasificación.

## Integrantes

- Samir Recalde Molina
- Juan Camilo Gallego Granada

**Institución:** Universidad del Quindío  
**Asignatura:** Seminario de Investigación  
**Proyecto:** AgroTech  
**Año:** 2026

## Modelos utilizados

### YOLO

Se utiliza un detector previamente entrenado para identificar las hojas dentro de las fotografías. El modelo genera cuadros delimitadores y puntuaciones de confianza para cada detección.

Repositorio de Ultralytics:  
https://github.com/ultralytics/ultralytics

Modelo de detección utilizado:  
https://huggingface.co/GovRang/tomato-leaf-model

### MobileSAM

Se utiliza para separar las hojas del fondo de las fotografías a partir de las regiones detectadas por YOLO.

Repositorio:  
https://github.com/ChaoningZhang/MobileSAM

### Vision Transformer (ViT V4)

Se utiliza para clasificar las hojas en siete categorías. La versión V4 empleada en el proyecto se obtuvo combinando los pesos de dos versiones anteriores desarrolladas durante los experimentos.

Modelo ViT de referencia:  
https://huggingface.co/wellCh4n/tomato-leaf-disease-classification-vit

## Categorías de clasificación

1. Sana
2. Moho foliar
3. Tizón tardío
4. Tizón temprano
5. Mancha bacteriana
6. Septoriosis
7. Virus del mosaico

## Conjunto de datos

Durante el desarrollo del clasificador se utilizaron imágenes del conjunto PlantDoc, además de imágenes adicionales de tizón temprano.

Repositorio de PlantDoc:  
https://github.com/pratikkayal/PlantDoc-Dataset

## Funcionamiento del sistema

1. Se carga una fotografía de una planta de tomate.
2. YOLO detecta las hojas y genera cuadros delimitadores.
3. MobileSAM separa las hojas del fondo mediante máscaras.
4. Se generan recortes rectangulares y segmentados.
5. ViT V4 clasifica las imágenes de las hojas.
6. El programa guarda las predicciones y las imágenes procesadas.

## Ejecución del cuaderno

El programa principal se encuentra en el archivo:

`EXP010_YOLO_MobileSAM_V4_CPU.ipynb`

Está diseñado para ejecutarse en Google Colab utilizando CPU.

### Instrucciones

1. Abrir el cuaderno en Google Colab.
2. Instalar las dependencias mediante la primera celda del cuaderno.
3. Autorizar el acceso a Google Drive.
4. Indicar la ubicación de una fotografía de tomate.
5. Configurar la ruta del clasificador ViT V4.
6. Ejecutar las celdas del cuaderno en orden.
7. Revisar las imágenes y los archivos generados.

### Archivos necesarios para ViT V4

El clasificador requiere:

- `config.json`
- `model.safetensors`
- `preprocessor_config.json`

Estos archivos deben estar almacenados en una misma carpeta.

**Descarga del checkpoint V4:** [Agregar enlace de Google Drive con permiso de lectura].

El detector YOLO y MobileSAM se descargan automáticamente durante la ejecución, siempre que exista conexión a Internet.

## Resultados obtenidos

En una evaluación exploratoria con 114 imágenes de PlantDoc, el clasificador ViT V4 obtuvo:

- Exactitud: 61,40 %
- F1 macro: 0,6169
- Recall macro: 63,70 %
- Imágenes correctamente clasificadas: 70 de 114

Estos resultados corresponden a la evaluación del clasificador y no representan la exactitud del sistema completo en condiciones reales de invernadero.

## Archivos generados

El sistema guarda diferentes archivos para revisar el procesamiento:

- `foto_clasificada.jpg`: fotografía con las detecciones y clasificaciones.
- `hoja_NNN_rectangulo.jpg`: recorte rectangular.
- `hoja_NNN_segmentada.jpg`: hoja procesada mediante MobileSAM.
- `hoja_NNN_mascara.png`: máscara de segmentación, cuando está disponible.
- `mosaico_comparativo.jpg`: comparación visual de los recortes.
- `resultados.csv`: resultados individuales de las hojas.
- `TODAS_las_hojas.csv`: resultados generales.
- `resumen.json`: resumen de la ejecución.

## Limitaciones

El sistema es un prototipo experimental y todavía necesita evaluaciones adicionales.

Se requiere medir el rendimiento del detector YOLO, evaluar la calidad de las máscaras generadas por MobileSAM y comprobar el funcionamiento del sistema completo mediante fotografías nuevas revisadas por especialistas.

Las clasificaciones generadas no reemplazan el diagnóstico de un profesional.

## Documentación

La documentación completa del proyecto, con la metodología, los resultados y las conclusiones, se encuentra en la carpeta `documentacion` de este repositorio.

## Referencias principales

- Ultralytics: https://github.com/ultralytics/ultralytics
- YOLOv8: https://docs.ultralytics.com/models/yolov8
- MobileSAM: https://github.com/ChaoningZhang/MobileSAM
- Vision Transformer: https://arxiv.org/abs/2010.11929
- PlantDoc: https://github.com/pratikkayal/PlantDoc-Dataset

---

**Universidad del Quindío – Seminario de Investigación – AgroTech, 2026.**
