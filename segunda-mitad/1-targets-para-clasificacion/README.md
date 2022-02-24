# Targets para clasificación
Ahora vamos a convertir nuestro problema en uno de clasificación. Para ello necesitaremos un target nuevo.

## Objetivo
Entender cómo podemos arreglar problemas de nuestros targets transformando a un target discreto.

## Contexto
Hemos terminado de hacer una regresión que utiliza una variable continua. Aunque esto es totalmente válido - muchas veces es también interesante transformar el problema a uno de clasificación - la predicción de valores discretos en vez de valores continuos. Esto puede tener varias ventajas:

* Muchas veces nuestras decisiones se basan en una clasificación de algo (finalmente la toma de decisiones es algo binario, o haces algo o no lo haces)
* Muchas veces es más fácil de interpretar una clasificación
* Las clasificaciones sufren menos de los datos "extremos"

Para empezar nos toca volver a hacer un análisis similar al que hicimos para determinar el target para nuestra regresión.

## Estrategia

1. Revisar el objetivo del modelo, el análisis que hicimos para el target de regresión y la evaluación de nuestro modelo - recoger los principales debilidades / problemas que encontramos
2. Entender cómo podemos eliminar estos problemas transformando el problema en una clasificación
3. Transformar las variables relevantes en variables discretas y analizar la validez de estas nuevas variables

## Preguntas importantes para guiar

* ¿Cómo podemos eliminar problemas de "outliers" utilizando clasificación?
* No solo tenemos clasificación binaria - cómo afectará el problema si transformamos en una clasificación multiclase?
* ¿Qué debilidades tiene transformar el problema en uno de clasificación?

## Que esperamos tener?
Unos ejemplos de variables que se podrían utilizar para una clasificación.

## Ejemplos para arrancar motores

### Analizando los extremos
Buscamos popularidad - al fin y al cabo no nos importa tanto si un tweet tiene 10 o 20 likes, pero 10 o 10,000.

```python
print(tweets_data.nlikes.quantile([0.5, 0.8, 0.9, 0.95]))
tweet_data['muchos_likes'] = tweet_data.nlikes >= tweets_data.nlikes.quantile(0.9)

print(tweet_data.groupby('muchos_likes).nlikes.describe())
```