# Evaluacion
Ahora hemos entrenado unos modelos y hemos hecho la exploracion inicial. En la primera mitad del curso tuvimos una introduccion muy breve a la evaluacion y ahora vamos a profundizar mucho más.

## Objetivo
Establecer un marco general para evaluar nuestro problema y tener muy claro como de bueno son algunos modelos.

## Contexto
La evaluación es fundamental para entender como funcionan nuestros modelos y como van a funcionar en el mundo real. Es un tema muy importante tanto para regresion como para clasificacion, pero es algo mas interesante en los problemas de clasificacion porque podemos evaluar la prediccion final o la probabilidad.

### Evaluando la prediccion final
Lo más facil de entender es la evaluación de la prediccion final - es simplemente contestar a la pregunta "cuantas veces hemos acertado?". Si deciamos que 10 tweets eran populares y al final solo 3 lo fueron - pues hemos acertado en 30% de los casos. Esto se llama el accuracy y es la metrica mas comun que hay.

#### Matrices de confusion
En realidad esto es solo una vista simple del problema. En realidad para clasificacion binaria tenemos 4 combinaciones de prediccion: predecir que "los 1s son 1s", "los 0s son 0s", "los 1s son 0s" o que "los 0s son 1s". Estas combinaciones se resumen en la [matrix de confusion](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html). La matrix de confusion compara las distintas combinaciones de prediccion y realidad.

Es importante considerar estas combinaciones porque en muchos casos no es lo mismo equivocarse predicciendo un evento que no predecirlo. El ejemplo más tipico es en [medicina](https://www.statisticssolutions.com/wp-content/uploads/2017/12/rachnovblog-1024x413.jpg) - es mucho mejor equivocarse diciendo que alguien este enferma cuando no lo esta (le hacemos mas pruebas y ya esta), que decir que no esta cuando sí que esta (puede resultar en la muerte).

Hay muchas metricas que resumen la matrix de confusion y los mas tipicos (aparte del accuracy) son los errores de tipo 1 y 2. En general es muy interesante considerar "que porcentaje de los casos positivos soy capaz de predecir" a la vez de "que porcentaje de los casos que predigo que sean positivos realmente lo son". Es decir, cuantos de los casos positivos "capto" y como de "pura" es mi prediccion. Estas dos metricas se llaman la recall y precision y en como norma general - para subir uno, hay que bajar el otro! Las pruebas medicas suelen tener muy buen recall para sacrificar precision (poco error tipo 2 y mas error tipo 1).

### Evaluando la probabilidad
Evaluar la prediccion final es similar a evaluar la decision final que tomarias dado tu prediccion. Esto esta bien, pero la decision que tomamos depende de la probabilidad que predicimos. Segun el umbral final que elejimos, podemos tener una infinidad de decisiones posibles con solo una prediccion de probabilidad - entonces tiene sentido evaluar esta probabilidad directamente, independiente de cualquier "decision".

Una cosa conceptual importante que tener en cuenta es que no existe una probabilidad "verdadero" - solo tenemos 0s y 1s, entonces no podemos hacer algo como un "accuracy" de la probabilidad como lo que hacemos en regresion y la evaluacion de la prediccion final. 

#### Evaluando directamente
Existen varios tipos de metrica que evaluan la "calidad" de la probabilidad que hemos predicho de forma muy directa. La idea es premiar o castigar más cuando mas / menos probabilidad predecimos en el caso de acertar / equivocar. Si el target real era un 1 y predecimos 99% de probabilidad, esto es mejor que cuando acertamos prediciendo 10%.

La metrica mas tipica para esto es el "log loss". Cuando mas bajo - mejor! Esta metrica se utiliza en los algoritmos de entrenamiento en varios casos.

#### Evaluando en el contexto de futuras decisiones

Problema de overfitting

Nota: es posible conseguir entrenar un modelo muy "bueno" con estos datos, pero el objetivo siempre es aprender. Por esto es clave comparar diferentes modelos y entender las diferencias.

## Estrategia

1. ...
2. ...
3. ...

## Preguntas importantes para guiar

* ...

## Que esperamos tener?
...

## Ejemplos para arrancar motores

### EXAMPLE 1
...

```python
pass
```