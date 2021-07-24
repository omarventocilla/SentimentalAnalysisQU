# SentimentalAnalysisQU
Análisis de Sentimientos para el Quechua usando Cross Language

El código dentro del notebook de jupyter SentimentalAnalysis tiene como entradas los word embeddings tanto del inglés como del quechua. Dichos archivos se encuentran en la página de fasttext (https://fasttext.cc/docs/en/crawl-vectors.html)
También toma como entrada el corpus etiquetado del inglés, que para este caso es el archivo dataset_en.csv en donde se ha recopilado comentarios y opiniones acerca del covi-19 en el idioma inglés junto con el sentimiento que dicho comentario expresa, etiquetándolo con un valor de 0:negativo; 1:neutro o 2:positivo. Por otro lado se tiene también el corpus del quechua en donde se ha recopilado de la misma manera comentarios acerca del covid-19 en el idioma quechua junto con su sentimiento.

# Metodología
Lo primero que se realiza es limpiar los datos del idioma inglés, para este caso las oraciones. Se eliminan todos los caracteres especiales, emojis, tweets, etiquetaciones, entre otros que no aportan al entrenamiento del modelo. Luego, se tokeniza cada una de las palabras dentro de las oraciones ya limpias. Asimismo, se eliminan aquellas palabras de paro de las oraciones (stopwords) para tener solo aquellas palabras relevantes para el análisis.

Para el análisis de las palabras, se realizan dos funciones que permiten lematizar (relacionar palabras según su contexto) y hallar la raíz sintáctica de las palabras. También se define una función que permite hallar los textos relacionados a cada token dependiendo del tipo de operación que se requiera (lemmatize o stemmer).

Al ya tener los fastText para el inglés y el quechua, se define una función que permita leer el contenido de dichos documentos. Se crea una función que permita dicha acción y que retorne las palabras con su índice, los índices a palabras y las palabras a un mapa vectorial.

Luego, se crea una función que permite tokenizar las reseñas en base a un marco de datos para su posterior uso. También se crea una función que permite obtener el sentimiento relacionado a un texto el cual retornará valores entre -1 y 1. Para el caso, se definen 3 sentimientos: 0, 1 y 2; los cuales tienen rangos de -1 a -0.65, -0.65 a 0.35 y de 0.35 a 1, respectivamente. A su vez, se genera una función que permite representar los documentos como vectores en base a su longitud. Con esto, se genera otra función que simplemente convierte una entrada en representación one-hot para su tratamiento.

Finalmente, para poder evaluar el modelo descrito se crea una función que lee en primera instancia el fastText del quechua mediante la función definida anteriormente, para luego tokenizar el marco de datos relativo a la función para definir el conjunto de datos de prueba, se generan los vectores de prueba al convertir a vector los parámetros correspondientes, y se definen los one-hot de prueba con la función pertinente. Luego, simplemente evalúa el desempeño del modelo realizado, devolviendo la pérdida del modelo y su precisión.
