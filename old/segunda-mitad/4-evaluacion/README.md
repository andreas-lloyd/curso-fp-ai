# Evaluacion
Ahora hemos entrenado unos modelos y hemos hecho la exploración inicial. En la primera mitad del curso tuvimos una introducción muy breve a la evaluación y ahora vamos a profundizar mucho más.

## Objetivo
Establecer un marco general para evaluar nuestro problema y tener muy claro cómo de bueno son algunos modelos.

## Contexto
La evaluación es fundamental para entender cómo funcionan nuestros modelos y cómo van a funcionar en el mundo real. Es un tema muy importante tanto para regresión como para clasificación, pero es algo más interesante en los problemas de clasificación porque podemos evaluar la predicción final o la probabilidad.

### Evaluando la predicción final
Lo más fácil de entender es la evaluación de la predicción final - es simplemente contestar a la pregunta "cuántas veces hemos acertado?". Si decíamos que 10 tweets eran populares y al final solo 3 lo fueron - pues hemos acertado en el 30% de los casos. Esto se llama el accuracy y es la métrica más común que hay.

#### Matrices de confusion
En realidad esto es solo una vista simple del problema. En realidad para clasificación binaria tenemos 4 combinaciones de predicción: predecir que "los 1s son 1s", "los 0s son 0s", "los 1s son 0s" o que "los 0s son 1s". Estas combinaciones se resumen en la [matrix de confusion](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html). La matriz de confusión compara las distintas combinaciones de predicción y realidad.

Es importante considerar estas combinaciones porque en muchos casos no es lo mismo equivocarse prediciendo un evento que no predecirlo. El ejemplo más tipico es en [medicina](https://www.statisticssolutions.com/wp-content/uploads/2017/12/rachnovblog-1024x413.jpg) - es mucho mejor equivocarse diciendo que alguien este enferma cuando no lo esta (le hacemos mas pruebas y ya esta), que decir que no esta cuando sí que esta (puede resultar en la muerte).

Hay muchas métricas que resumen la matriz de confusión y las más típicas (aparte del accuracy) son los errores de tipo 1 y 2. En general es muy interesante considerar "qué porcentaje de los casos positivos soy capaz de predecir" a la vez de "qué porcentaje de los casos que predigo que sean positivos realmente lo son". Es decir, cuántos de los casos positivos "capto" y como de "pura" es mi predicción. Estas dos métricas se llaman la recall y precisión y como norma general - para subir uno, hay que bajar el otro! Las pruebas médicas suelen tener muy buen recall para sacrificar precisión (poco error tipo 2 y más error tipo 1).

### Evaluando la probabilidad
Evaluar la predicción final es similar a evaluar la decisión final que tomarías dado tu predicción. Esto está bien, pero la decisión que tomamos depende de la probabilidad que producimos. Según el umbral final que elegimos, podemos tener una infinidad de decisiones posibles con solo una predicción de probabilidad - entonces tiene sentido evaluar esta probabilidad directamente, independiente de cualquier "decisión".

Una cosa conceptual importante que tener en cuenta es que no existe una probabilidad "verdadero" - solo tenemos 0s y 1s, entonces no podemos hacer algo como un "accuracy" de la probabilidad como lo que hacemos en regresión y la evaluación de la predicción final. 

#### Evaluando directamente
Existen varios tipos de métrica que evalúan la "calidad" de la probabilidad que hemos predicho de forma muy directa. La idea es premiar o castigar más cuando más / menos probabilidad predecimos en el caso de acertar / equivocar. Si el target real era un 1 y predecimos 99% de probabilidad, esto es mejor que cuando acertamos prediciendo 10%.

La métrica más típica para esto es el "log loss". Cuando mas bajo - mejor! Esta métrica se utiliza en los algoritmos de entrenamiento en varios casos (por ejemplo, la regresión logística).

#### Evaluando en el contexto de futuras decisiones
La otra manera de evaluar la probabilidad es simular las decisiones que tomaremos considerando una serie de umbrales de probabilidades. Por ejemplo, qué pasaría si cortamos a 50%? Y a 10%? Si conseguimos resumir el resultado de todas estas simulaciones, vamos a entender la calidad de la probabilidad dentro de un contexto que es más fácil de interpretar.

La métrica más común para hacer esto es el "AUC" o "área debajo de la curva ROC". Es una métrica que simplemente resume el "trade off" entre precisión y recall y cuando más alto, más alto serán estas dos métricas como un conjunto. Es una de las métricas más comunes y nos va a proporcionar mucha más información que un simple accuracy. 

##### Simular
Otra cosa que podemos hacer es hacer una simulación financiera de los diferentes umbrales que hemos hecho - esto requiere un poco más de creatividad pero es una manera muy buena de resumir y vender nuestro modelo. Algo típico sería decir "si utilizamos nuestro modelo... 

* vamos a acertar un `X%` del tiempo, ganando `$X*Y`,
* vamos a equivocarnos un `%x` del tiempo, perdiendo `$x*y`
* un humano tarda `T` horas en completar este trabajo, acierta `X'`, se equivoca `x'` y cobra `$H` la hora, haciendo por hora `C` casos
* nuestro modelo entonces gana por "caso" `(X*Y - $x*y) - (X'*Y - $x'*y) + H/C` (con algún extra por "adelantar" más casos en el mismo tiempo que es más difícil de estimar)
..."

Normalmente nos equivocamos un poco más y acertamos un poco menos que un humano - pero los humanos tardan muchísimo más tiempo en completar la tarea (potencialmente x1000 veces) y entonces acabamos ahorrando mucho dinero. Por este motivo en el sur de EEUU utilizan humanos para recoger fruta y utilizan máquinas en el norte (según Reddit).

##### Top X
En algunos problemas también puede tener sentido hacer evaluaciones de los "top X" predicciones. Por ejemplo - si vamos a escribir contenido para contestar a ciertos Tweets, no nos interesa que acertemos en todos los Tweets (no podemos escribir contenido para todo) - pero sí que nos interesa mucho que los 10 Tweets que pensamos que van a ser más populares realmente sean populares. Entonces podríamos calcular el accuracy entre los primeros 10 Tweets que más probabilidad tengan. 

#### Optimizando el umbral
Hemos estado hablando de varias formas de evaluar las predicciones, trabajando con la probabilidad. Un punto sutil pero muy importante es que **después de evaluar y elegir nuestro modelo favorito, siempre debemos especificar un umbral para nuestras probabilidades y evaluar la predicción final con este umbral**. 

Es decir, podemos pasar toda la evaluación mirando solo la probabilidad, pero cuando entregamos el trabajo al cliente, no podemos decir "toma, unas probabilidades muy bien predichas" - debemos decir "a partir de X% tienes que hacer...". Y claro, en este contexto, debemos también incluir una evaluación final de las "decisiones" que hacemos con tal umbral (por ejemplo, el accuracy, el recall etc.). 

En general lo que hacemos es elegir el umbral que saca las mejores métricas en el contexto de futuras decisiones (tipo, yo elijo un umbral de 70% y no 50% porque mi recall es mejor...).

### Overfitting
El otro aspecto fundamental de la evaluación es detectar y limitar el overfitting. Overfitting es cuando nuestro modelo "aprende demasiado" de unos datos y las predicciones que hace no se generalizan a los datos exteriores. Es como si estuviera memorizando los patrones exactos de los datos en vez de aprender el patrón general.

Es un tema muy amplio pero tiene mucho peligro con los modelos más "flexibles" (y los más flexibles suelen ser los más poderosos). Es fundamental que en el proceso de evaluación tengamos claro hasta qué punto van a generalizar nuestros resultados al mundo externo.

La señal más estándar de que no vamos a generalizar es que las métricas cambian mucho entre training / validación / test. Por eso es muy importante dividir los datos.

### Predicciones multiclase
Muchos han elegido utilizar un target con varias clases. Esto es algo muy interesante! Lo único "malo" es que hay que trabajar un poco más a la hora de evaluar porque para cada clase vamos a tener una matriz de confusión entera!

Como es especialmente interesante estudiar la curva ROC, unos comentarios:

* Aqui hay [cosas intersantes](https://stackoverflow.com/questions/45332410/roc-for-multiclass-classification) sobre como evaluar ejemplos multiclase
* La documentacion de scitkit-learn tambien tiene [unos ejemplos interesantes](https://scikit-learn.org/stable/auto_examples/model_selection/plot_roc.html)
* El AUC se puede calcular utilizando diferentes técnicas de medias:
    * Coger la media de AUC si consideramos que una predicción es acertada o no (convertirlo en pseudo-binario)
    * Coger la media de AUC de todas las posibles "parejas" de predicciones
* En general vamosa  tener peores métricas cuando es multiclase porque hay más opciones - puede ser útil centrarnos en la clase que vemos más importante

### Entender dónde están los problemas
Hasta ahora hemos descrito una evaluación muy generalista, pero parte de la evaluación también es entender dónde están nuestros problemas y donde podemos mejorar. Esto puede tomar varias formas, por ejemplo:

* Analizar los conjuntos de datos donde peor métrica sacamos (por ejemplo, quizás sacamos peor accuracy para Tweets en inglés que en castellano)
* Analizar las predicciones que peor métrica sacamos (puede ser que nos equivocamos mucho cuando no tenemos muy seguro que predecir y la probabilidad es cerca del 50%)

Una vez entendemos las debilidades de nuestro modelo, podemos actuar o simplemente dejarlo como un comentario para una iteración al futuro. Cosas típicas que podemos hacer son:

* Limitar el modelo a ciertos tipos de datos, donde mejor predice
* Crear procesos de decisiones distintas según la predicción (si pensamos que la probabilidad de presencia de una enfermedad no es bastante alta / baja, podemos mandar para más pruebas)

Dentro de este proceso también podemos incluir métodos de evaluación de cómo entender las variables importantes y sus efectos.

## Estrategia

1. Entrenar varios modelos para comparar
2. Elegir las métricas adecuadas 
3. Sacar las métricas y analizar los problemas que tenemos en el modelo - comentando y aplicando (cuando podamos) las mejoras que vemos factibles

Nota: es posible conseguir entrenar un modelo muy "bueno" con estos datos, pero el objetivo siempre es aprender. Por esto es clave comparar diferentes modelos y entender las diferencias.

## Preguntas importantes para guiar

* ¿Qué métricas tendrán más sentido mirar en la evaluación?
* ¿Cómo vamos a asegurar que no hay overfitting?
* ¿Cómo podemos incorporar el contexto de negocio en la evaluación?

## Que esperamos tener?
Un resumen de la bondad de nuestros modelos y unas mejoras para hacer (o ahora o en el futuro).

## Ejemplos para arrancar motores

### Medir el [AUC](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_auc_score.html#sklearn.metrics.roc_auc_score)

```python
from sklearn.metrics import roc_auc_score
probability = model.predict_proba(X)[:,1]
score = roc_auc_score(y, probability)
```

También se puede especificar un `max_fpr` para ignorar los umbrales que resultan en demasiados falsos positivos.

### Dibujar la curva de precisión recall
La curva de precision recall es muy similar a [la curva ROC](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.plot_roc_curve.html), pero por mi es más facil de interpretar.

```python
test['predictions_1'] = model_1.predict_proba(X_test)
test['predictions_2'] = model_2.predict_proba(X_test)

results = []
renames = {0 : 'recall', 1 : 'precision', 2 : 'threshold'}
for i in range(1, 6):
    result = pd.DataFrame(sklearn.metrics.precision_recall_curve(test[target], test[f'predictions_{i}'])).transpose().rename(columns=renames)
    result['prediction_number'] = str(i)
    results.append(result)
    
results = pd.concat(results) 

results['threshold'] = results.threshold.round(3)

results = results.groupby(['prediction_number', 'threshold']).head(1)

# Esto es simplemente algo que puede que salga mas bonito el gráfico - dependiendo del caso, puede que no sea necesario
results['recall_diff'] = results.groupby('prediction_number').recall.diff()
results['precision_diff'] = results.groupby('prediction_number').precision.diff()

c = (results.recall_diff >= 0)
graph = (
    pn.ggplot(results[c], pn.aes(x='recall', y='precision', color='prediction_number'))
    + pn.geom_line(size=1.4)
)

graph.draw();
```

### Entender nuestras variables
Con la regresión logística y modelos de árboles, hay formas muy buenas para entender el resultado:

* Ver los coeficientes de la regresión (`model.coef_, model.intercept_`)
* Ver el arbol en si y las importancias de cada variable

```python
import sklearn.tree
from matplotlib import pyplot as plt

feature_names = X.columns

# Hace falta un modelo de tipo "decision tree"
plt.figure(figsize=(25, 12))
sklearn.tree.plot_tree(
    tree_model, fontsize=12, feature_names=feature_names, class_names=['No es popular', 'Es popular'], max_depth=4, 
    impurity=False, proportion=True, precision=2
)
plt.show()

graph_data = pd.DataFrame(
    [(imp, variable) for imp, variable in zip(tree_model.feature_importances_, feature_names)], 
    columns=['importance', 'variable']
).sort_values('importance', ascending=False)

limit = 15 # Para no ver todas las variables si tenemos muchas
graph = (
    pn.ggplot(graph_data.head(limit), pn.aes(x='variable', y='importance')) 
    + pn.geom_col()
    + pn.coord_flip()
    + pn.theme(figure_size=(7, 5))
    + pn.scale_x_discrete(limits=graph_data.head(limit).variable.unique()[::-1])
)

graph.draw();
```
