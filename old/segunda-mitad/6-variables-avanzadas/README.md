# Variables avanzadas
Más allá de los típicos features que utilizamos existen unas variables que contienen más información pero son más difíciles de construir.

## Objetivo
Entender cómo podemos incorporar variables más complejas en nuestros modelos.

## Contexto
Hay algunas variables que podemos utilizar en nuestros modelos que tienen más poder que una variable normal. Ejemplos de estos tipos de variables son:

* Conteos de actividad historico de usuarios
* Análisis del contexto de un ejemplo
* Técnicas de reducción de dimensiones y / o clustering
* Análisis de texto e imágenes

No es necesario para nada utilizar estas técnicas, pero son interesantes de considerar y aportan mucho valor en algunos problemas.

### Conteos de actividad histórico
Normalmente en nuestros problemas hay un "actor" principal. Esto puede ser un usuario, un cliente, un sistema, un animal... En general es la "cosa" que causa nuestro comportamiento de interés.

Este actor es muy importante por varios motivos:

* Nunca vamos a tener todas las características que describen el actor (en muchos casos, sería imposible - imaginate tener una variable para cada segundo de la vida de un humano)
* Los comportamientos del pasado se repiten muchas veces

Por ejemplo, si quisieras predecir notas de exámenes, saber las notas que obtuvieron los estudiantes en sus exámenes anteriores sería de gran utilidad.

Las variables típicas que vamos a ver de este estilo son:

* Número de veces que el actor ha hecho algo (por ejemplo, nuestro comportamiento de interés) en el pasado
* La media de algo en el pasado

Aquí puede sugerir la duda: no es tramposo utilizar el target para predecir el target? Pero lo importante aquí es que usamos el pasado para predecir el futuro - si sabemos el resultado de un ejemplo anterior a la hora de predecir, es totalmente válido. En sistemas de recomendaciones, por ejemplo, los gustos del pasado se utilizan para predecir los gustos del futuro. Los modelos clásicos de forecasting todos utilizan una variante del pasado para predecir el futuro.

Pero tenemos que tener mucho cuidado a la hora de evaluar nuestro modelo:

* Puede ser difícil construir nuestras variables en el conjunto de validación y test (no podemos utilizar ejemplos del futuro para calcular las variables!)
* Si nos basamos enteramente en el pasado de un actor, no vamos a saber actuar frente a un actor nuevo
* Si unos pocos actores se repiten mucho, es posible que nuestro modelo aprenderá a detectar los actores en vez de aprender el comportamiento
* Siempre vamos a tener unos ejemplos sin historico y tenemos que tener cuidado con el motivo de no tener datos (estamos recogiendo toda la actividad de un cliente desde su registración, o simplemente cortando una query de SQL?)

### Análisis del contexto
De forma similar a analizar el pasado, podemos analizar el presente en ejemplos similares. Es efectivamente lo mismo, pero analizando el pasado (seguramente más reciente) de los otros actores en el conjunto de datos.

Esto es lógico porque el contexto de los demás probablemente sea similar al contexto de nuestro actor. 

Un ejemplo muy sencillo de esto es el "feed" de Netflix de "trending now" - simplemente están recogiendo lo que les gusta a los demás pensando que te gustara a ti.

Estas variables también tendrán una misma forma que la actividad histórica (número medio de X para otros usuarios etc.) y los problemas también son los mismos.

### Reducción de dimensiones y clustering
Realmente estos son 2 campos de análisis de datos, pero lo importante aquí es pensar que podemos utilizar estas técnicas en nuestros modelos.

Cosas que podemos hacer incluyen:

* En vez de entrenar utilizando nuestras variables, podemos entrenar sobre el resultado de las dimensiones reducidas
* Entrenar un clustering para detectar grupos de interés y utilizar la asignación de estos grupos en el modelo
* Utilizar un clustering para reducir el enfoque del modelo que queremos entrenar

Puedes pensar que "utilizar una técnica compleja seguramente ayudará a mi modelo!" pero te equivocas. Hay que considerar que si estamos utilizando las mismas variables para generar las nuevas variables (por ejemplo, clusters) que entrenan el modelo, no habrá mucha información nueva para un modelo más complejo.

En el caso de tener un modelo débil o nuevos datos, sí que puede ser útil ya que vamos a introducir conceptos nuevos para el modelo.

También hay que considerar que estas técnicas pueden permitirnos utilizar menos variables en el modelo final que ayudará la interpretación - pero solo cuando tenemos una buena interpretación de los resultados de las otras técnicas (si tenemos 10 clusters sin ningún sentido, el modelo final no será fácil de entender tampoco).

### Análisis de texto e imágenes
Otros campos enteros que están evolucionando mucho. 

Es posible que tengamos datos de texto o imágenes en nuestro conjunto de datos y puede que aporten algo de valor para nuestro modelo. Lo difícil es entender cómo incorporar estos datos con las demás variables que tenemos.

Hay 2 maneras principales de hacer esto:

* Entrenar un modelo que solo trabaja con los textos / imágenes y utilizar la predicción como variable del modelo
* Crear variables que representan la información de los textos / imágenes

Aquí hay muchas cosas que podemos hacer:

* Utilizar técnicas clásicas de [TF-IDF](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) o [term document matrix](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html) para extraer una representación cruda de los textos
* Utilizar modelos ya hechos para representar los textos / imágenes (por ejemplo, [embeddings](https://machinelearningmastery.com/develop-word-embeddings-python-gensim/) o [ImageNet](https://pyimagesearch.com/2016/08/10/imagenet-classification-with-python-and-keras/))
* Utilizar técnicas de reducción de dimensiones sobre las representaciones crudas
* Simplemente pillar unas características básicas de los textos / imágenes (largo de las frases, presencia de palabrotas...)

No podemos cubrir ni un 1% de estos campos, pero lo dejamos aquí porque son interesantes en general.

## Estrategia

1. Elegir algo que nos parece interesante probar
2. Implementar una lógica para aprovechar de esta variable en el entrenamiento
3. Evaluar el modelo nuevo, pero teniendo mucho cuidado con cómo hemos construido la variable

## Preguntas importantes para guiar

* ¿Qué características del pasado o del contexto son interesantes?
* Van a ser más importantes las características del pasado / contexto o de los imágenes / textos?
* ¿Cómo podemos evitar problemas a la hora de evaluar?
* ¿Cuánto realmente ayudan nuestras variables especiales?

## Que esperamos tener?
Unas variables extra que ayudan al modelo

## Ejemplos para arrancar motores

### Entrenar un modelo con solo el texto del Tweet

```python
from sklearn.feature_extraction.text import CountVectorizer

# Ojo, haz una mezcla de idiomas
vectorizer = CountVectorizer(min_df=3, strip_accents='unicode', token_pattern=r'\w{1,}', ngram_range=(1, 2), stop_words='english')

vectorizer.fit(train['tweet'])

model = RandomForestClassifier(random_state=1)

model.fit(vectorizer.transform(train['tweet']), train['target'])

predictions = model.predict(vectorizer.transform(test['tweet']))

print((predictions == test['target']).mean())
```
(que esperas que sea el resultado entrenando con solo el tweet?)

### Utilizar reducción de dimensiones y clustering

```python
from sklearn.decomposition import PCA
from sklearn.manifold import TSNE


# Primero entrenamos un TSNE
variables = [col for col in users if users[col].dtypes in [int, float] and col not in ['id_user']]

ncomponents = 2
tsne_pipeline = Pipeline(
    [
        ('scaler', preprocessing.StandardScaler()),
        ('pca', PCA(random_state=0)),
        ('tsne', TSNE(ncomponents, random_state=0))
    ]
)

cols = ['component_' + str(i + 1) for i in range(ncomponents)]
transformed_data = pd.DataFrame(tsne_pipeline.fit_transform(users[variables]), columns=cols)

# Y ahora un Kmeans
X_variables = ['component_1', 'component_2']

kmeans_tsne_pipeline = Pipeline(
    [
        ('scaler', preprocessing.StandardScaler()),
        ('cluster', KMeans(n_clusters=5, random_state=0))
    ]
)

kmeans_tsne_pipeline.fit(transformed_data[X_variables])
predictions = kmeans_tsne_pipeline.predict(transformed_data[X_variables])


transformed_data['predictions_kmeans_5_scaler'] = predictions

# Ahora combinamos la transformación con los datos originales de los tweets
cols_tweets = ['followers', 'video', 'id_user', 'target']
cols_trans = ['id_user', 'predictions_kmeans_5_scaler', 'component_1', 'component_2']
combined_data = tweets[cols_tweets].merge(transformed_data[cols_trans], on='id_user')

model = LogisticRegression()
model.fit(combined_data[['followers', 'video', 'predictions_kmeans_5_scaler']], transformed_data['target'])
predictions = model.predict(combined_data[['followers', 'video', 'predictions_kmeans_5_scaler']], transformed_data['target'])
```

### ¿Cuántos likes ha tenido el usuario en el pasado?
Un ejercicio para ti...