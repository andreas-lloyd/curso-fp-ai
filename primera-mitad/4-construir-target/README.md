# Construir el target
Un paso fundamental del entrenamiento de un modelo es elegir y construir el target que vamos a predecir.

## Objetivo
Entender bien los candidatos que tenemos para el target y entender cómo construirlo.

## Contexto
El target es fundamental para cualquier problema supervisado de machine learning. Siempre empezamos con un objetivo en mente y el target tiene que reflejar este objetivo. No siempre es obvio cómo hacer esto, pero siempre tenemos que buscar la señal en nuestros datos que refleja la realidad que estamos intentando predecir.

El target también es el dato que tiene que estar mejor preparado, porque va a afectar todo el proceso de modelado.

Nota que en la primera mitad del año vamos a centrarnos en la regresión, pero no tenemos que limitarnos a este tipo de problema por ahora.

## Estrategia

1. Tener claro el objetivo de nuestro modelo
2. Resumir lo que sabemos de los datos y cómo podemos mostrar que algo es "popular"
3. Considerar varios candidatos y detallar los pros, contras y los pasos que tendremos que hacer para preparar este target 


## Preguntas importantes para guiar

1. Cómo impacta la selección del target sobre el modelo? 
2. Cómo cambiaría la predicción con las diferentes transformaciones?
3. Si nuestro target se "comporta mal", cómo afecta al modelo?

## Que esperamos tener?
Unos candidatos muy claros para nuestro target, listos para poder analizar correlaciones y variables relevantes.

## Ejemplos para arrancar motores

### Número de replies
Las respuestas pueden ser muy interesantes porque muestra un "engagement" muy fuerte - pero es una variable realmente continua?

```python
print((tweet_data.nreplies == 0).mean())

# Y esto que significa?
print(tweet_data.loc[tweet_data.nreplies == 0, ['nlikes', 'nretweets']].describe())

cats = [-1, 0, 1, 5, 50, 500, 5000, 50000, tweet_data.nreplies.max() + 99999]
labels = [bin_lim for bin_lim in cats[1:-1]] + [f'More than {cats[-2]}']
tweet_data['nreplies_cats'] = pd.cut(tweet_data.nreplies, cats, labels=labels, include_lowest=True)

graph_data = tweet_data.groupby('nreplies_cats').id.nunique().reset_index()
graph_data['percentage'] = graph_data.id / graph_data.id.sum()

#from mizani.formatters import percent_format

graph = (
  pd.ggplot(graph_data, pn.aes(x='nreplies_cats', y='percentage')) 
  + pn.geom_col() 
  + pn.scale_y_continuous(labels=percent_format()) 
  + pn.coord_flip()
)
graph.draw();
```
Qué pasaria si intentamos una regresion con este target?

Qué otros problemas podemos encontrar?

### Número de likes
Los likes también parecen interesantes - pero habrán valores extremos?

```python
tweet_data['dummy'] = 'Número de likes'

graph = (
pn.ggplot(tweet_data, pn.aes(x='dummy', y='nlikes'))
+ pn.geom_boxplot() + pn.xlab('') + pn.coord_cartesian(ylim=(0, 1000))
)

graph.draw();
```
Cómo podemos interpretar el boxplot?

