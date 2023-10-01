# Análisis de datos
Básicamente todo el proceso de crear un modelo se puede considerar como analizar datos. Aquí nos referimos más específicamente al proceso de ganar conocimiento sobre los datos que vamos a trabajar.

## Por qué?
Para las decisiones que vamos a tomar en el proceso del modelado, necesitamos conocer bien el contexto. Parte del contexto viene de nuestro conocimiento externo y otra parte de nuestro conocimiento de los datos. En el mundo real, esto es un proceso muy continuo que no para. Cuanto más conocimiento de los datos, más oportunidades saldrán para mejorar nuestras soluciones.

## Técnicas
En general hay muchísimas cosas que podemos hacer. Siempre buscamos describir las diferentes variables y las relaciones entre ellas. Unos ejemplos son:

* Mirar la distribución de variables (medias, outliers, boxplots, distribuciones...)
* Agregar conteos y medias de una variable, agrupando por otras (conteos históricos, medias de valores por grupos...)


## Ejemplos
```python
data.SalePrice.describe(percentiles=[0.01, 0.99])

data.groupby('SaleCondition').SalePrice.agg(['count', 'mean'])

data['had_remodel'] = data.YearRemodAdd > data.YearBuilt
remod_price = data.groupby('had_remodel').SalePrice.mean().reset_index()

graph = pn.ggplot(remod_price, pn.aes(x='had_remodel', y='SalePrice')) + pn.geom_col()
graph
```