# Buscando las variables relevantes
Tenemos que encontrar los factores que influyen sobre nuestro target porque estos van a ser las entradas de nuestro modelo.

## Objetivo
Entender qué variables tienen poder predicitivo para nuestro target y cómo podemos sacar lo mejor de ellos.

## Contexto
Entendemos los datos. Tenemos más claro cual va a ser nuestro target (o targets). Ahora tenemos que entender qué variables de nuestros datos van as ser los que queremos utilizar en el modelo y de qué forma queremos utilizarlas.

Algunos dirian que lo mejor es utilizar todas las variables que tenemos disponibles y ya esta, pero esto puede ser peligroso porque:

* El modelo sera mucho mas dificil de interpretar
* Hay mucho mas posibilidad de errores y "over fitting"
* Seguramente algunas variables son utiles, pero solo bajo ciertas transformaciones

## Estrategia

1. Pensar que factores pueden influir sobre nuestro target
2. Identificarlos en los datos y recordar lo que vimos en el analisis inicial
3. Analizar como varia el target con los factores que hemos elegido

## Preguntas importantes para guiar

* Que son las variables que probablemente sean las mejores?
* Como se puede determinar que un factor es relevante para predecir el target?
* Como sabemos que son las mejores variables?
* Que transformacions podemos aplicar para mejorar los resultados?

## Que esperamos tener?
Una vision clara de las variables entrantes a nuestro modelo y las transformaciones que queremos aplicar.

## Ejemplos para arrancar motores

### El numero de followers
Llevamos meses diciendo que los tweets de cuentas con mas followers tendran mas popularidad, pero es cierto?
```python
tweet_data = pd.read_csv(tweet_file)
twitter_users = pd.read_csv(handles_file)

keys = ['user_id', 'id']
target = "nlikes"
variable = "followers"

tweet_data = tweet_data.merge(twitter_users[[keys[1], variable]], left_on=keys[0], right_on=keys[1])

print(tweet_data[[target, variable]].corr())

xmax = tweet_data[variable].quantile(0.95)
ymax = tweet_data[target].quantile(0.95)
(
    pn.ggplot(tweet_data, pn.aes(x=variable, y=target)) 
    + pn.geom_smooth(method="lm", color='red') + pn.geom_point(alpha=0.2) 
    + pn.xlim(0, xmax) + pn.ylim(0, ymax)
)
```

### Los videos hacen las cosas mas populares? Depende del idioma?
```python
import numpy as np

target = "nreplies"
variable = "video"

print(tweet_data.groupby(variable)[target].describe())

languages = tweet_data.language.value_counts().index[:6]
tweet_data["language_reduced"] = np.where(tweet_data.language.isin(languages), tweet_data.language, "others")
variable = ["language_reduced", "video"]
print(tweet_data.groupby(variable)[target].describe())
```
