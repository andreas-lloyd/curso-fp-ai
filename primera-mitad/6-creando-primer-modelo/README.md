# Creando nuestro primer modelo
Vamos a progresar y crear nuestra primera regresión.

## Objetivo
Crear un modelo que predice la popularidad de un tweet y sacar las predicciones.

## Contexto
Hemos progresado mucho:

* Entendemos nuestro data set
* Sabemos qué variables representan la popularidad y conocemos los problemas que vamos a encontrar
* Tenemos claro qué variables son potenciales predictores de nuestro target

Ahora toca lo que hemos venido aquí para hacer: entrenar un modelo. Lo que siempre hay que tener claro en nuestras cabezas es que el modelo final es solo 50% del "entregable" a nuestro cliente - la otra parte es la evaluación de cómo va a hacer su trabajo este modelo. No comprarías un coche sin hacer un test drive y ver opiniones primero verdad?

Esta parte del proyecto se puede hacer en 5 líneas o en 500, con 2 variables o 100, entrenando 1 modelo o 5 - lo fundamental es que seguimos un proceso correcto que va a permitir una evaluación posterior que tenga sentido. Si no tenemos claro más o menos como de bueno va a ser nuestro modelo con datos nuevos, no contará para nada nuestro esfuerzo.

Esta parte está tan vinculada con la parte de evaluación que es probable que ya adelantamos parte de la evaluación (el último paso) para hacer esta parte mejor.

## Estrategia
Ahora las cosas son un poco más simples y robóticos - ya hemos hecho lo difícil en las partes anteriores (por esto dicen que crear el modelo es solo 5% del esfuerzo). Ahora vamos a

1. Tener claro qué variables de entrada y el target que queremos para el modelo
2. Construir los pasos de preparación de datos para que nuestro modelo se puede entrenar (y de la mejor forma)
3. Entrenar nuestro modelo y predecir con ello

Podemos repetir estos pasos varias veces con diferentes combinaciones - de hecho - esto es lo más habitual.

## Preguntas importantes para guiar

* ¿Cuáles son los requisitos básicos para las variables de entrada al modelo? ¿Cómo puedo entrenar sin que me de errores? (haz lo minimo primero!)
* ¿Cuáles son los otros pasos de preparación de datos que pueden mejorar el resultado?
* ¿Cómo se entrenan modelos con scikit-learn? (usar otras librerías si queráis!)
* ¿Cómo puedo guardar un modelo ya entrenado?
* ¿Cómo se puede sacar predicciones de mis modelos?
* ¿Cuáles son los pasos **muy importantes** para asegurar una evaluación posterior buena? ([hint](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html))

## ¿Qué esperamos tener?
Unas predicciones que podemos evaluar en la siguiente parte. Necesitamos por lo menos predicciones de un modelo - pero sería interesante tener varios para comparar. Crear un nuevo modelo puede ser tan simple como modificar las variables de entrada.

## Ejemplos para arrancar motores

### Lo más mínimo para entrenar un modelo
```python
from sklearn.linear_model import LinearRegression

y = '' # Tu target aqui
X = ['', ''] # Tus variables aqui

model = LinearRegression() # Elegir el modelo
model.fit(tweets_data[X], tweets_data[y]) # Entrenar el modelo

predictions = model.predict(tweets_data[X]) # Predecir con el modelo

# Miramos a ver que tal...
tweets_data['predictions'] = predictions

tweets_data['difference'] = (tweets_data[y] - tweets_data.predictions)

print(tweets_data[[y, 'predictions', 'difference']].describe())
print('\n')
print(tweets_data[[y, 'predictions', 'difference']].corr())
```
Así de fácil (sólo 6 líneas y lo podríamos haber hecho en 3)! Pero esto es lo minimo de lo mínimo, se puede mejorar el proceso mucho:

* Tratamiento de datos -> Para asegurar que el modelo hace lo esperado y no hay datos raros afectando al entrenamiento
* Creación de variables -> Para dar más poder predictivo y también arreglar problemas de los datos
* Utilizar pipelines -> Hacer que el código sea más reutilizable y estable
* Separación train / test -> Mejorar el proceso de evaluación
* Probar otros modelos -> Mejor poder predictivo
