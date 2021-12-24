# Evaluando nuestro primer modelo
Ahora hemos entrenado un modelo y vamos a hacer una evaluacion basica. Como parte de esto, tambien vamos a hacer unas mejoras de nuestro modelo.

## Objetivo
Entender cómo funciona nuestro modelo y si predice bien.

## Contexto
Acabamos de entrenar nuestros primeros modelos y hemos dicho que una parte fundamental de este proceso es evaluar como funciona. Esta evaluacion la vamos a utilizar para:

* Mejorar nuestros modelos
* Tener claro cual funciona mejor
* Explicar a nuestro cliente lo que hemos logrado

La evaluacion es en realidad muy abierto y las mejores evaluaciones tienen en cuenta el objetivo de negocio que tenemos. Los importantes puntos a tener en cuenta son:

* Los pasos del entrenamiento que nos permite hacer una buena evaluacion
* Las metricas que utilizamos para evaluar
* Como tener en cuenta el contexto de negocio que tenemos

Pero lo que es comun para todo es que para evaluar si realmente nuestro modelo "aprende" y es capaz de "predecir" algo, tenemos que probarlo con "datos nuevos".

## Estrategia

0. Montar bien el proceso de entrenamiento para permitir una buena evaluacion
1. Recoger las predicciones que tenemos y el target (los valores "verdaderos")
2. Elegir las metricas, analisis y visualizaciones que nos parecen mejores para evaluar los resultados
3. Ejecutar el segundo paso y resumir los resultados
4. Entender que potenciales mejoras hay y incorporarlos en el proceso el entrenamiento (y evaluar de nuevo!)

Hay un punto "0" porque esta parte esta muy vinculada con la anterior (el proceso de entenar el modelo).

## Preguntas importantes para guiar

* Qué significa predecir bien? Cómo sabes si podemos mejorar el resultado o no?
* ¿Cuáles son las metricas habituales para evaluar regresiones? ([hint](https://scikit-learn.org/stable/modules/model_evaluation.html))
* Qué problemas hay con las metricas estandares? Si visualizamos los datos, entendemos mejor que esta pasando?
* Siempre debemos elegir el modelo que maximiza / minimiza las metricas? Hay otros factores que tambien son importantes?
* Teniendo en cuenta el objetivo de negocio, que metricas tienen mas o menos sentido?

## ¿Qué esperamos tener?
Una manera objetivo de comprar los modelos que hemos entrenado que nos dan una buena idea de como podrian funcionar en el "mundo real"

## Ejemplos para arrancar motores

### Comparar nuestras predicciones con la realidad
```python
graph_data = pd.DataFrame({'realidad' : tweet_data[y], 'predicciones' : predictions})

graph = pn.ggplot(graph_data, pn.aes(x='realidad', y='predicciones')) + pn.geom_point() + pn.geom_smooth(method="lm", color='red')
graph.draw();
```

### Utilizar un baseline
```python
from sklearn.metrics import median_absolute_error

tweet_data['baseline'] = tweet_data[y].mean()

print(median_absolute_error(tweet_data[y], tweet_data['baseline']))
print(median_absolute_error(tweet_data[y], predictions))

```
Si la diferencia es muy baja, que quiere decir sobre nuestro modelo?
