# Targets para clasificacion
Ahora vamos a convertir nuestro problema en uno de clasificacion. Para ello necesitaremos un target nuevo.

## Objetivo
Entender como podemos arreglar problemas de nuestros targets transformando a un target discreto.

## Contexto
Hemos terminado de hacer una regresion que utiliza una variable continua. Aunque esto es totalmente valido - muchas veces es tambien interesante transformar el problema a uno de clasificacion - la prediccion de valores discretos en vez de valores continuos. Esto puede tener varias ventajas:

* Muchas veces nuestras decisiones se basan en una clasificacion de algo (finalmente la toma de decisiones es algo binario, o haces algo o no lo haces)
* Muchas veces es más facil de interpretar una clasificacion
* Las clasificaciones sufren menos de los datos "extremos"

Para empezar nos toca volver a hacer un analisis similar al que hicimos para determinar el target para nuestra regresion.

## Estrategia

1. Revisar el objetivo del modelo, el analisis que hicimos para el target de regresion y la evaluacion de nuestro modelo - recoger los principales debilidades / problemas que encontramos
2. Entender como podemos eliminar estos problemas transformando el problema en una clasificacion
3. Transformar las variables relevantes en variables discretas y analizar la validez de estas nuevas variables

## Preguntas importantes para guiar

* Como podemos eliminar problemas de "outliers" utilizando clasificacion?
* No solo tenemos clasificacion binaria - como afectara el problema si transformamos en una clasificacion multiclase?
* Que debilidades tiene transformar el problema en uno de clasificacion?

## Que esperamos tener?
Unos ejemplos de variables que se podrian utilizar para una clasificacion.

## Ejemplos para arrancar motores

### Analizando los extremos
Buscamos popularidad - al fin y al cabo no nos importa tanto si un tweet tiene 10 o 20 likes, pero 10 o 10,000.

```python
print(tweets_data.nlikes.quantile([0.5, 0.8, 0.9, 0.95]))
tweet_data['muchos_likes'] = tweet_data.nlikes >= tweets_data.nlikes.quantile(0.9)

print(tweet_data.groupby('muchos_likes).nlikes.describe())
```