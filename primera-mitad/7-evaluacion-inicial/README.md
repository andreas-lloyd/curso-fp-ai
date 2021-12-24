# Evaluando nuestro primer modelo
Ahora hemos entrenado un modelo y vamos a hacer una evaluación básica. Como parte de esto, también vamos a hacer unas mejoras de nuestro modelo.

## Objetivo
Entender cómo funciona nuestro modelo y si predice bien.

## Contexto
Acabamos de entrenar nuestros primeros modelos y hemos dicho que una parte fundamental de este proceso es evaluar cómo funciona. Esta evaluación la vamos a utilizar para:

* Mejorar nuestros modelos
* Tener claro cuál funciona mejor
* Explicar a nuestro cliente lo que hemos logrado

La evaluación es en realidad muy abierta y las mejores evaluaciones tienen en cuenta el objetivo de negocio que tenemos. Los importantes puntos a tener en cuenta son:

* Los pasos del entrenamiento que nos permite hacer una buena evaluación
* Las métricas que utilizamos para evaluar
* Como tener en cuenta el contexto de negocio que tenemos

Pero lo que es común para todo es que para evaluar si realmente nuestro modelo "aprende" y es capaz de "predecir" algo, tenemos que probarlo con "datos nuevos".

## Estrategia

0. Montar bien el proceso de entrenamiento para permitir una buena evaluación
1. Recoger las predicciones que tenemos y el target (los valores "verdaderos")
2. Elegir las métricas, análisis y visualizaciones que nos parecen mejores para evaluar los resultados
3. Ejecutar el segundo paso y resumir los resultados
4. Entender que potenciales mejoras hay e incorporarlos en el proceso del entrenamiento (y evaluar de nuevo!)

Hay un punto "0" porque esta parte está muy vinculada con la anterior (el proceso de entrenar el modelo).

## Preguntas importantes para guiar

* ¿Qué significa predecir bien? ¿Cómo sabes si podemos mejorar el resultado o no?
* ¿Cuáles son las métricas habituales para evaluar regresiones? ([hint](https://scikit-learn.org/stable/modules/model_evaluation.html))
* ¿Qué problemas hay con las métricas estándares? Si visualizamos los datos, entenderemos mejor qué está pasando?
* Siempre debemos elegir el modelo que maximiza / minimiza las métricas? ¿Hay otros factores que también son importantes?
* Teniendo en cuenta el objetivo de negocio, ¿qué métricas tienen más o menos sentido?

## ¿Qué esperamos tener?
Una manera objetivo de comprar los modelos que hemos entrenado que nos dan una buena idea de cómo podrían funcionar en el "mundo real"

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
Si la diferencia es muy baja, ¿qué quiere decir sobre nuestro modelo?
