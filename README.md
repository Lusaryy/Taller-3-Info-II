# 4.5. INFORME Y DISCUSIÓN

**1. Descripción del proyecto**

Este proyecto consiste en desarrollar una aplicación en Python capaz de leer, extraer, organizar y analizar metadatos de archivos DICOM, utilizando librerías de software libre como pydicom, numpy y pandas.
La idea es simular una parte del flujo real de un sistema PACS, automatizando la carga de archivos, la obtención de información relevante del estudio (como paciente, modalidad, fecha, tamaño de la imagen, etc.) y un análisis sencillo de intensidad promedio de los píxeles.
Todo el código está estructurado en programación orientada a objetos para mantener la lógica clara y modular.


**2. Explica brevemente por qué DICOM y HL7 son cruciales para la interoperabilidad en salud y en qué se diferencian conceptualmente.**

En informática médica, la interoperabilidad no es algo insignificante, sino que es lo que permite que hospitales, modalidades de imagen, sistemas administrativos y aplicaciones clínicas puedan comunicarse sin depender del fabricante.
DICOM se encarga del mundo de las imágenes médicas. Define:
  - Cómo se guarda la imagen
  - Cómo se estructuran los metadatos
  - Cómo se envían los estudios entre dispositivos (modalidades, PACS, workstations)
    
HL7, por otro lado, se enfoca en la información clínica y administrativa: datos del paciente, órdenes médicas, resultados de laboratorio, historia clínica, etc.
Aunque son estándares distintos, se complementan. Gracias a ellos un estudio puede viajar desde un tomógrafo hasta un PACS, y luego a una estación de trabajo, sin que nada se “pierda” o quede incompatible.


**3. Pregunta teórica: ¿Qué relevancia clínica o de pre-procesamiento podría tener el análisis de de la distribucion de intensidades en una imágen médica?**

Analizar la distribución de intensidades en una imagen médica es más importante de lo que parece. A nivel clínico y de preprocesamiento permite:
- Evaluar la calidad del estudio (por ejemplo, detectar imágenes demasiado oscuras o saturadas)
- Identificar patrones generales de tejido, ya que diferentes intensidades pueden corresponder a densidades o características específicas
- Normalizar o estandarizar imágenes antes de aplicar algoritmos de segmentación, filtrado o aprendizaje automático
- Detectar artefactos o valores atípicos que podrían afectar el diagnóstico o el procesamiento posterior

Incluso un cálculo tan básico como la intensidad promedio ya puede orientar si la imagen está dentro de rangos normales o si tiene problemas de adquisición.


**4. Mencionar dificultades encontradas y la importancia de las herramientas de Python para el analisis de datos médicos.**
Dificultades en el taller:
- Tags DICOM ausentes o anonimizados, lo que nos obligó a manejar excepciones para evitar que el programa falle
- Advertencias del estándar DICOM, especialmente con valores inválidos del tipo UI, que ocupaban mucho espacio en el output
- Variabilidad entre estudios, ya que no todos los archivos contienen los mismos metadatos o estructuras internas
- Carga de múltiples archivos, que requiere recorrer directorios completos y manejar errores de lectura

Las herramientas de Python que facilitan bastante este trabajo:
- Pydicom permite leer el contenido de un archivo DICOM como si fuera un objeto de Python, acceder a los tags y manejarlos sin convertirlos manualmente
- Numpy hace posible procesar los valores de píxeles con velocidad y precisión
- Pandas organiza los metadatos en un DataFrame, lo cual vuelve el análisis y la consulta muchísimo más prácticos


