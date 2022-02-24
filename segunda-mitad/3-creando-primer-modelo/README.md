# Creando el primer modelo
Vamos muy rápido y ya tenemos nuestro target. Como antes, vamos a entrenar nuestros primeros modelos para empezar ya la evaluación y todo lo que viene después.

## Objetivo
Tener unas primeras predicciones de unos modelos iniciales.

## Contexto
En esta parte del curso queremos centrarnos en temas más avanzados como la evaluación y optimización. Para llegar a este punto es importante tener un baseline de modelos para ir tirando. Ya hemos investigado las variables y targets, así que estamos listos para entrenar modelos.

### Probabilidad vs. target final
Realmente no hay mucha diferencia entrenando un modelo para clasificación que para regresión así que el código y los conceptos importantes son iguales. La diferencia más importante es que ahora podemos predecir un valor final o una probabilidad:

* Predecir la probabilidad es justo esto - la probabilidad de que nuestro evento ocurre
* Muchas veces una probabilidad no es lo más útil y tenemos que "decidir" si nuestro evento va a ocurrir - esto lo hacemos fijando un umbral en la probabilidad: si la probabilidad es mayor que X, yo creo que el evento va a ocurrir
* Si predecimos nuestro valor final de forma directa, lo único que hace nuestro modelo es usar un umbral predeterminado de 50%

En general es más útil predecir la probabilidad por varios motivos:

* Siempre puedes fijar un umbral de 50% y recuperar la "predicción final" que te habría dado el modelo
* En general, no siempre vas a querer utilizar el 50% (¿Cruzarias la calle si tuvieras un 49.99% de probabilidad de ser atropellado? ¿Jugarías a la lotería si tuvieras una probabilidad de 10% de ganar?)
* Una evaluación completa va a tener en cuenta tanto las predicciones finales como las probabilidades - es peor equivocarse prediciendo una probabilidad de 99% o de 51%?

Aquí hay un tema avanzado de "predecir" vs. "decidir" - los modelos están diseñados y creados para predecir bien, no para tomar decisiones!

Otros puntos importantes a tener en cuenta:

* Si la mayoria de tus datos tienen un valor del target (por ejemplo 99% False y 1% True) tienes un problema "desequilibrado" y estás casi obligado a utilizar la probabilidad, porque muy pocas veces vas a tener un valor por encima de 50% (ejemplo de la lotería...)
* Ciertos modelos predicen una probabilidad más "real" que otros - árboles de decisión, por ejemplo, no predicen una probabilidad real, mientras una regresión logística sí
* Si tenemos un problema "multiclase" también existen probabilidades! La predicción final suele ser o la clase que más probabilidad tiene, o la que más tiene si tiene más probabilidad del umbral (que pueden ser distintos para cada clase - o quizás ninguna clase llega a tener bastante probabilidad y predecimos "nulo")

### Modelos más poderosos
Ahora somos casi expertos en cómo entrenar modelos, así que vamos a dejar un poco más de margen para explorar modelos más poderosos. Para clasificación unos ejemplos muy típicos de modelos que se utilizan son:

* Regresión logística - el modelo más clásico para este tipo de problema
* Modelos de arboles - un mundo entero de muchos modelos que se basan en los [arboles de decision](https://scikit-learn.org/stable/modules/tree.html) utilizando tecnicas de "[ensembling](https://scikit-learn.org/stable/modules/ensemble.html)"
* Las redes neuronales - los modelos más flexibles que hay

En otras semanas vamos a explorar mucho más el tema de optimización y la elección de modelos, pero ahora puede ser buen momento para hacer una exploración inicial de estos modelos más poderosos.

Lo más importante que hay que tener en cuenta es el "overfitting". Los modelos más poderosos son más flexibles, permitiendo un entrenamiento más preciso para nuestro problema, pero corremos el riesgo de ajustar demasiado y perder el poder de predecir bien con datos ajenos.

Hay muchas maneras de evitar este problema, pero lo más importante es detectar que no está pasado - para esto es clave la división de los datos en train y validación! Si las métricas de evaluación salen muy dispares en los diferentes conjuntos de datos, es muy probable que haya overfitting.

### Más allá de una predicción binaria
Existen diferentes tipos de predicción - los más comunes siendo predicción binaria y multiclase. También existen las predicciones "multi-etiqueta" - donde un ejemplo puede tener varias etiquetas. Para acercarnos a los diferentes tipos, [scitkit-learn nos ayuda mucho](https://scikit-learn.org/stable/modules/multiclass.html).

## Estrategia

1. Tener claro qué variables de entrada y el target que queremos para el modelo
2. Construir los pasos de preparación de datos para que nuestro modelo se puede entrenar (y de la mejor forma)
3. Entrenar nuestro modelo y predecir con ello

Y probar diferentes cosas!

## Preguntas importantes para guiar

* ¿Cómo predecimos una probabilidad en vez de un target concreto?
* ¿Cómo podemos transformar nuestra probabilidad en una predicción concreta?
* ¿Cuáles son los parámetros que podemos ajustar para limitar el overfitting?

## Que esperamos tener?
Unas predicciones que podemos evaluar en profundidad en la siguiente parte.

## Ejemplos para arrancar motores

### Lo más mínimo para entrenar un modelo

```python
from sklearn.linear_model import LogisticRegression

y = '' # Tu target aqui
X = ['', ''] # Tus variables aqui

model = LogisticRegression() # Elegir el modelo
model.fit(tweets_data[X], tweets_data[y]) # Entrenar el modelo

predictions = model.predict(tweets_data[X]) # Predecir con el modelo
probability = model.predict_proba(tweets_data[X])

# Miramos a ver qué tal...
tweets_data['predictions'] = predictions
tweets_data['probability'] = probability[:, 1]

tweets_data['correct'] = (tweets_data[y] == tweets_data.predictions)

print(tweets_data[[y, 'predictions', 'correct']].describe())
```
