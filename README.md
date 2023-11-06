# TUIA - Procesamiento del Lenguaje Natural - 2023

## Trabajo Práctico Nº 1
"Procesamiento del Lenguaje"


## Alumnos
* Timoteo García
* Claudia Leguiza
* Miguel Mussi


## Consignas
### Ejercicio 1
Construir un dataset haciendo web scraping de páginas web de su elección.
* Definir 4 categorías de noticias/artículos.
* Para cada categoría, extraer los siguientes datos de 10 noticias diferentes:
  * url (sitio web donde se publicó el artículo)
  * título (título del artículo)
  * texto (contenido del artículo)

**Recomendaciones**: elegir blogs para evitar los límites de lectura para los medios que exigen suscripción. Investigue sobre el archivo robots.txt y téngalo en cuenta. Considere también espaciar las consultas para evitar saturar el sitio.

Utilizando los datos obtenidos construya el dataset en formato csv. 

### Ejercicio 2
Utilizando los datos de título y categoría del dataset del ejercicio anterior, entrenar un modelo de clasificación de noticias en categorías específicas.

### Ejercicio 3
Para cada categoría, realizar las siguientes tareas:
* Procesar el texto mediante recursos de normalización y limpieza.
* Con el resultado anterior, realizar conteo de palabras y mostrar la importancia de las mismas mediante una nube de palabras.

Escribir un análisis general del resultado obtenido.

### Ejercicio 4
Use los modelos de embedding propuestos sobre el final de la Unidad 2 para evaluar la similitud entre los títulos de las noticias de una de las categorías.

Reflexione sobre las limitaciones del modelo en base a los resultados obtenidos, en contraposición a los resultados que hubiera esperado obtener.

### Ejercicio 5
Escriba un programa interactivo que, según la categoría seleccionada por el usuario, devuelva un resumen de las noticias incluidas en ella.

Justifique la elección del modelo usado para tal fin.

**Opcional**: Investigar y programar un bot de Telegram que entregue un resumen de noticias del blog de su elección.

Recomendamos el uso de [pyTelegramBotAPI](https://github.com/eternnoir/pyTelegramBotAPI). 


# Desarrollo del TP

## Web Scraping

El scraping de los textos se realiza sobre el portal de noticias [Clarin](https://www.clarin.com). En particular, en las secciones correspondientes a Economía, Política, Sociedad y Deportes. 
Para este trabajo se extraen diez (10) artículos de cada categoría y se procesan con las herramientas provistas por la cátedra.

**NOTA**: Los primeros bloques de código que corresponden al web scraping, la confección del dataframe y la generación del archivo csv **SE EJECUTAN UNA SOLA VEZ**, por lo que pueden aparecer comentados en el proyecto. A partir de allí, el resto del trabajo se realiza sobre la carga y procesamiento de esos mismos datos.

### DataFrame | CSV
Luego de realizado el scraping, los datos son volcados a un dataframe que servirá para exportar un archivo csv. Este proceso se realiza por única vez (o cada vez que se deseen actualizar los registros de las noticias). 

Para agilizar las tareas posteriores de procesamiento, el resto del código ofrece la posibilidad de importar archivos de tipo csv a un nuevo dataframe. Este paso es necesario para permitir trabajar con diferentes archivos, sin necesidad de realizar el scraping cada vez.

### Procesamiento de los datos
En esta sección, se lleva a cabo el procesamiento de los datos extraídos del web scraping. Este paso es esencial para preparar los textos de las noticias para su posterior análisis.

Se realizan tareas de conversión a minúsculas, eliminación de espacios en blanco, de acentos y signos de puntuación.

Este proceso de limpieza garantiza que los textos estén listos para ser procesados de manera consistente y se minimizan las posibles fuentes de ruido en el análisis posterior. Los datos limpios se utilizan como punto de partida para tareas de NLP, como la aplicación del modelo de clasificación.


## Modelo de Clasificación
En esta sección, se describe el proceso de creación y evaluación del modelo de clasificación de textos. Las tareas realizadas incluyen:

**Preparación de los Datos**: Se seleccionan los títulos de las noticias (X) y las etiquetas de categoría (y) de la fuente de datos. Además, se realiza una transformación para asegurar que los títulos estén en un formato adecuado.

**Creación del Pipeline**: Se crea un flujo de trabajo (pipeline) que incluye dos pasos: la vectorización de los títulos utilizando CountVectorizer y la clasificación utilizando LogisticRegression. Esto permite la transformación de los títulos en representaciones numéricas y su posterior clasificación.

**División y de Conjunto de Datos**: El conjunto de datos se divide en conjuntos de entrenamiento y prueba (80% para entrenamiento y 20% para prueba) utilizando train_test_split.

**Entrenamiento del Modelo**: El modelo se entrena utilizando el conjunto de entrenamiento (x_train, y_train) a través del pipeline.

**Evaluación del Modelo**: Se evalúa el rendimiento del modelo utilizando el conjunto de prueba (x_test, y_test). Se calcula la precisión (accuracy) y se genera un informe de clasificación que incluye métricas como precisión, recall y F1-score. Además, se prueba el modelo utilizando un conjunto de noticias nuevas para verificar su capacidad de predicción en la clasificación de noticias en las secciones correspondientes.

![Métricas del Modelo](/modelo_metricas.png)

## Normalización y Limpieza

**Eliminación de Palabras de Parada**: Se descargan las palabras de parada (stop words) en español utilizando la biblioteca nltk y se implementa una función que elimina las palabras de parada de los textos. Las palabras son tokenizadas y luego se filtran las que están en la lista de palabras de parada, lo que ayuda a reducir el ruido en los textos.

**Tokenización y Lematización**: Se realiza la tokenización de los textos, dividiendo el texto en palabras o tokens individuales. Para la lematización, se utiliza el modelo de lenguaje en español de spaCy. La lematización consiste en reducir las palabras a su forma base o lema, lo que simplifica la comparación de palabras similares.

**Proceso de Normalización**: Se prueba un proceso de normalización adicional que incluye la eliminación de acentos, conversión a minúsculas, eliminación de signos de puntuación y reducción de las palabras a su forma raíz (stemming) mientras se eliminan las palabras de parada.

**Eliminación de Columnas Innecesarias**: Las columnas "título" y "enlace" son eliminadas de los datos, ya que no son necesarias para el análisis posterior.

## Análisis del texto
En esta sección se realiza un recuento de las palabras de los textos y se muestra la importancia de ellas mediante una nube de palabras para cada categoría realizada con la librería WordCloud.

![Deportes](/nube_deportes.png)
![Economía](/nube_economia.png)
![Política](/nube_politica.png)
![Sociedad](/nube_sociedad.png)


## Análisis de similitudes
En esta sección, se lleva a cabo la evaluación de similitudes entre los títulos de noticias pertenecientes a diferentes temas. Las tareas realizadas son las siguientes:

**Selección del Modelo de Embeddings**: Se utiliza el modelo SentenceTransformer 'distiluse-base-multilingual-cased-v1' para generar representaciones vectoriales de los títulos de noticias. Este modelo es capaz de codificar oraciones en vectores de alta dimensión que capturan la semántica de las oraciones.

**Agrupación de Títulos por Tema**: Los títulos se agrupan por tema. Esto permite comparar la similitud entre los títulos dentro de un mismo tema y entre diferentes temas.

**Cálculo de Similitud**: Se realizan la codificación de las oraciones, el cálculo de las puntuaciones de similitud del coseno entre los embeddings de todas las combinaciones de pares de títulos y el ordenamiento de mayor a menor.

**Presentación de Resultados**: Los resultados se presentan en una tabla que muestra los pares de títulos con las puntuaciones de similitud más altas organizados por categoría. 


## Resúmenes por categoría
En esta sección se realiza la generación de resúmenes de noticias por categoría. 

**Selección del Modelo de Generación de Resúmenes**: Se utiliza el modelo "csebuetnlp/mT5_multilingual_XLSum" para generar resúmenes de noticias. Este modelo es capaz de producir resúmenes multilingües de alta calidad. La elección de este modelo se justifica por su capacidad multilingüe, calidad, flexibilidad y rendimiento en la generación de resúmenes.

**Resúmenes de una categoría particular**: Se implementa un script preliminar que permite al usuario seleccionar una categoría en particular. El script genera resúmenes de todas las noticias que pertenecen a la categoría elegida. Esto facilita la obtención de resúmenes específicos para una categoría de noticias.

**Resúmenes Interactivos**: Se desarrolla otro script actualizado que brinda al usuario la capacidad de elegir una cantidad de noticias y su categoría. 



