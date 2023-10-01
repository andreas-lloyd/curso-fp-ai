# Las variables relevantes
Ahora tenemos una idea de los targets discretos que pueden servir para una clasificación. Toca entender qué variables influyen sobre nuestros targets.

## Objetivo
Entender qué factores influyen sobre nuestra clasificación.

## Contexto
Otra vez volvemos a un ejercicio similar a uno que hicimos para la regresión. Ahora como los targets son nuevos, toca volver a analizar las variables relevantes. Es muy posible que lo que antes era relevante sigue siendo relevante, pero tenemos cuidado porque:

* Alguna variable puede ser muy relevante para distinguir entre valores que ahora tienen la misma clasificación
* Variables que antes no eran muy útiles ahora pueden serlo
* Los outliers en las variables son menos importantes
* Nuevas transformaciones pueden ser útiles

## Estrategia
Realmente vamos a hacer algo similar al ejercicio que hicimos anteriormente.

1. Pensar que factores pueden influir sobre nuestro target - tomando como referencia el ejercicio pasado
2. Entender si unas transformaciones nuevas pueden ser útiles
3. Analizar cómo varía el target con los factores que hemos elegido

## Preguntas importantes para guiar

* ¿Cómo entendemos lo que es relevante para un target no continuo?

## Que esperamos tener?
Una visión clara de las variables entrantes a nuestro modelo y las transformaciones que queremos aplicar.

## Ejemplos para arrancar motores

### Followers
El número de followers era importante antes pero sufría de un problema de outliers - sigue siendo igual?

```python
graph = (
    pn.ggplot(tweets_data, pn.aes(x='muchos_likes', y='followers))
    + pn.geom_boxplot()
    + pn.coord_cartesian(ylim=(0, tweets_data.followers.quantile(0.95)))
)

graph.draw();
```