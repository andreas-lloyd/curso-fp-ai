# Construir el target
Un paso fundamental del entrenamiento de un modelo es elegir y construir el target que vamos a predecir.

## Objetivo
Entender bien los candidatos que tenemos para el target y entender como construirlo.

## Contexto
El target es fundamental para cualquier problema supervisado de machine learning. Siempre empezamos con un objetivo en mente y el target tiene que reflejar este objetivo. No siempre es obvio como hacer esto, pero siempre tenemos que buscar la señal en nuestros datos que refleja la realidad que estamos intentando predecir.

El target tambien es el dato que mejor tiene que estar preparado, porque va a afectar todo el proceso de modelado.

Nota que en la primera mitad del año vamos a centrarnos en regresion, pero no tenemos que limitarnos a solo este tipo de problema por ahora.

## Estrategia

1. Tener claro el objetivo de nuestro modelo
2. Resumir lo que sabemos de los datos y como podemos monstrar que algo es "popular"
3. Considerar varios candidatos y detallar los pros, contras y los pasos que tendremos que hacer para preparar este target 


## Preguntas importantes para guiar

1. Como impacta la seleccion del target sobre el modelo? 
2. Como cambiara la prediccion con los diferentes transformaciones?
3. Si nuestro target se "comporta mal", como afecta al modelo

## Que esperamos tener?
Unos candidatos muy claros para nuestro target, listo para poder analizar correlaciones y variables relevantes.

## Ejemplos para arrancar motores

## Número de replies
Las respuestas pueden ser muy interesantes porque muestra un "engagement" muy fuerte - pero es una variable realmente continua?

```python
print((tweet_data.nreplies == 0).mean())

# Y esto que significa?
print(tweet_data.loc[tweet_data.nreplies == 0, ['nlikes', 'nretweets']].describe())
```