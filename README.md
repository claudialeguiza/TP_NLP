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
[agregar]

## Modelo de Clasificación
[agregar]

## Normalización y Limpieza
[agregar]

## Análisis de similitudes
[agregar]

## Resúmenes por categoría
[agregar]



