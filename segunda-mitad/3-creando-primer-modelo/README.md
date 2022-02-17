# Creando el primer modelo
Vamos muy rapidos y ya tenemos nuestro target. Como antes, vamos a entrenar nuestros primeros modelos para empezar ya la evaluación y todo lo que viene despues.

## Objetivo
Tener unas primeras predicciones de unos modelos iniciales.

## Contexto
En esta parte del curso queremos centrarnos en temas más avanzados como la evaluacion y optimizacion. Para llegar a este punto es importante tener un baseline de modelos para ir tirando. Ya hemos investigado las variables y targets, asi que estamos listos para entrenar modelos.


### Probabilidad vs. target final
Realmente no hay mucha diferencia entrenando un modelo para clasificacion que para regresion asi que el codigo y los conceptos importantes son iguales. La diferencia más importante es que ahora podemos predicir un valor final o una probabilidad:

* Predecir la probabilidad es justo esto - la probabilidad de que nuestro evento ocurre
* Muchas veces una probabilidad no es lo más util y tenemos que "decidir" si nuestro evento va a ocurrir - esto lo hacemos fijando un umbral en la probabilidad: si la probabilidad es mayor que X, yo creo que el evento va a ocurrir
* Si predecimos nuestro valor final de forma directa, lo unico que hace nuestro modelo es usar un umbral predeterminado de 50%

En general es más util predecir la probabilidad por varios motivos:

* Siempre puedes fijar un umbral de 50% y recuperar la "prediccion final" que te habria dado el modelo
* En general, no siempre vas a querar utilizar 50% (cruzarias la calle si tuvieras un 49.99% de probabilidad de ser atropellado? Jugarias a la loteria si tuvieras una probabilidad de 10% de ganar?)
* Una evaluación completa va a tener en cuenta tanto las predicciones finales como las probabilidades - es peor equivocarse prediciendo una probabilidad de 99% o de 51%?

Aquí hay un tema avanzado de "predicir" vs. "decidir" - los modelos estan diseñados y creados para predicir bien, no para tomar decisiones!

Otros puntos importantes a tener en cuenta:

* Si la mayoria de tus datos tienen un valor del target (por ejemplo 99% False y 1% True) tienes un problema "desequilibrado" y estas casi obligado a utilizar la probabilidad, porque muy pocas veces vas a tener un valor por encima de 50%
* Ciertos modelos predicen una probabilidad más "real" que otros - arboles de decision, por ejemplo, no predicen una probabilidad real, mientras una regresion logistica si
* Si tenemos un problema "multiclase" tambien existen probabilidades! La prediccion final suele ser o la clase que más probabilidad tiene, o la que más tiene si tiene más probabilidad del umbral (que pueden ser distintos para cada clase)

### Modelos más poderosos
Ahora somos casi expertos en como entrenar modelos, asi que vamos a dejar un poco mas de margen para explorar modelos más poderosos. Para clasificación unos ejemplos muy tipicos de modelos que se utilizan son:

* Regresion logistica - el modelo más clasico para este tipo de problema
* Modelos de arboles - un mundo entero de muchos modelos que se basan en los [arboles de decision](https://scikit-learn.org/stable/modules/tree.html) utilizando tecnicas de "[ensembling](https://scikit-learn.org/stable/modules/ensemble.html)"
* Las redes neuronales - los modelos más flexibles que hay

En otras semanas vamos a explorar mucho más el tema de optimizacion y la eleccion de modelos, pero ahora puede ser buen momento para hacer una exploración inicial de estos modelos más poderosos.

Lo más importante que hay que tener en cuenta es el "overfitting". Los modelos más poderosos son más flexibles, permitiendo un entrenamiento más preciso para nuestro problema, pero corremos el riesgo de ajustar demasiado y perder el poder de predecir bien con datos ajenos.

Hay muchas maneras de evitar este problema, pero lo más importante es detectar que no está pasado - para esto es clave la division de los datos en train y validation!

## Estrategia

1. Tener claro qué variables de entrada y el target que queremos para el modelo
2. Construir los pasos de preparación de datos para que nuestro modelo se puede entrenar (y de la mejor forma)
3. Entrenar nuestro modelo y predecir con ello

Y probar diferentes cosas!

## Preguntas importantes para guiar

* Como predecimos una probabilidad en vez de un target concreto?
* Como podemos transformar nuestra probabilidad en una prediccion concreta?
* Que son los parametros que podemos ajustar para limitar el overfitting?

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

# Miramos a ver que tal...
tweets_data['predictions'] = predictions
tweets_data['probability'] = probability[:, 1]

tweets_data['correct'] = (tweets_data[y] == tweets_data.predictions)

print(tweets_data[[y, 'predictions', 'correct']].describe())
```
