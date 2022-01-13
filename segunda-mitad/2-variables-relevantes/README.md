# Las variables relevantes
Ahora tenemos una idea de que targets discretos pueden servir para una clasificacion. Toca entender que variables inluyen sobre nuestros targets.

## Objetivo
Entender que factores inluyen sobre nuestra clasificacion.

## Contexto
Otra vez volvemos a un ejercicio similar a uno que hicimos para la regresion. Ahora como los targets son nuevos, toca volver a analizar las variables relevantes. Es muy posible que lo que antes era relevante sigue siendo relevante, pero tenemos cuidado porque:

* Alguna variable puede ser muy relevante para distinguir entre valores que ahora tienen la misma clasificacion
* Variables que antes no eran muy utiles ahora pueden serlo
* Los outliers en las variables son menos importantes
* Nuevas transformaciones pueden ser utiles

## Estrategia
Realmente vamos a hacer algo similar al ejercicio que hicimos anteriormente.

1. Pensar que factores pueden influir sobre nuestro target - tomando como referencia el ejercicio pasado
2. Entender si unas transformaciones nuevas pueden ser utiles
3. Analizar como varia el target con los factores que hemos elegido

## Preguntas importantes para guiar

* Como entendemos lo que es relevante para un target no continuo?

## Que esperamos tener?
Una visión clara de las variables entrantes a nuestro modelo y las transformaciones que queremos aplicar.

## Ejemplos para arrancar motores

### Followers
El numero de followers era importante antes pero sufria de un problema de outliers - sigue siendo igual?

```python
graph = (
    pn.ggplot(tweets_data, pn.aes(x='muchos_likes', y='followers))
    + pn.geom_boxplot()
    + pn.coord_cartesian(ylim=(0, tweets_data.followers.quantile(0.95)))
)

graph.draw();
```