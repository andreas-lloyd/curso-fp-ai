# Optimización
Una parte importante del entrenamiento de modelos es la optimización de todos los aspectos del flujo. Hacer esto de forma estructurada es importante para no volvernos locos.

## Objetivo
Aprender a estructurar y ejecutar un proceso de optimización **sin** volvernos locos.

## Contexto
Durante todo este proceso largo han surgido muchas dudas tipo "es mejor hacer X o Y?" y la respuesta siempre ha sido "pruébalo!". Esto seria fácil si tuviéramos pocas opciones, pero entre el procesamiento de los datos, elección de variables y los hiperparametros de los modelos, hace falta algo más estructurado para comprobar todas las opciones.

### ¿Qué exactamente significa que algo sea mejor?
Siempre hay que considerar que no es fácil decir exactamente qué modelo es "mejor". Obviamente este tema está muy vinculado con la evaluación y tenemos que considerar varios factores:

* ¿Qué modelo es más robusto?
* ¿Qué modelo es más fácil de interpretar?
* ¿Qué modelo saca las mejores métricas?
* ¿Qué modelo entendemos mejor?
* Que modelo sera mas fácil de implementar?
* ¿Qué modelo es más fácil de debuggear y modificar?

No todas las respuestas van a ser 100% objetivas y cuando menos objetivo, más difícil va a ser automatizar y organizarnos.

### Automatizar la optimización
Para contestar a todo lo más objetivo vamos a automatizar el proceso de optimización. Es decir, para algunas de las preguntas de la evaluación, vamos a crear un proceso que busca el conjunto de las mejores decisiones que podemos tomar. Principalmente vamos a centrarnos en mejorar las métricas típicas de evaluación - pero también podríamos inventar otras métricas para reflejar la interpretabilidad, robustez, facilidad de implementación etc. (por ejemplo, número de variables...).

Hay varias maneras de crear este proceso y [muchos frameworks](https://towardsdatascience.com/10-hyperparameter-optimization-frameworks-8bc87bc8b7e3) para facilitarnos la vida pero somos aburridos asi que vamos a empezar mirando [lo basico en Scitkit-learn](https://scikit-learn.org/stable/modules/grid_search.html). En general todos se basan en la misma lógica:

* Entrenamos un modelo con unas opciones
* Evaluamos este modelo con nuestro proceso de evaluación y métricas
* Entrenamos otro modelo con otras opciones
* Evaluamos el nuevo modelo y comparamos con el primero
* El mejor modelo es el que saca las mejores métricas
* Repite el proceso para las opciones que queremos investigar

Normalmente las diferentes técnicas se diferencian en cómo eligen las diferentes opciones a probar. Cuantas más opciones probamos, más tardará el proceso.

#### Cross validation
Antes de empezar merece la pena hablar brevemente sobre cross validation (CV). CV es una técnica que nos permite generar varios conjuntos de train y validación de un solo set de train. Utilizamos los diferentes conjuntos para evaluar nuestro modelo varias veces - la métrica final siendo la media / mediana de todas.

La ventaja principal de esto es que no nos cegamos los resultados de la evaluación a un único conjunto de datos. Puede ser que por mala / buena suerte un modelo es mucho mejor para unos datos específicos y es mejor agregar en varios conjuntos.

Esto tiene mucho sentido en el contexto de la optimización porque vamos a estar probando muchos modelos y sería muy fácil optimizar el modelo para un conjunto de datos específicos en vez de optimizarlo a un nivel más generalizado. La desventaja es que tendremos que entrenar un modelo nuevo para cada conjunto de datos!

#### Grid search
La técnica más famosa de optimización es el grid search. Básicamente definimos los diferentes hiperparametros que queremos analizar y las diferentes opciones que queremos probar. Se crea un conjunto de todas las opciones posibles y se entrena el modelo para cada uno.

Por ejemplo, para un random forest queremos optimizar el número de árboles y la profundidad máxima. Nos parece guay mirar las opciones:

* 100, 500 y 1000 para numero de arboles
* 5, 10 y sin límite para la profundidad máxima

Se define un "grid" de:

* 100 arboles y 5 de profundidad, 100 árboles y 10 de profundidad, 100 árboles y sin límite
* 500 arboles y 5 de profundidad, 500 árboles y 10 de profundidad, 500 árboles y sin límite
* 1000 arboles y 5 de profundidad, 1000 árboles y 10 de profundidad, 1000 árboles y sin límite

Para las 9 opciones entrenamos 9 veces y nos quedamos con la combinación que obtiene el mejor (por ejemplo) AUC. Si utilizamos un "5 fold CV" entrenaremos 5 modelos para cada combinación y un modelo final con todos los datos para la mejor combinación.

Esto es muy simple y asegura que vamos a explorar exactamente el espacio que queremos. El problema es que ya estamos hablando de 9 x 5 modelos y solo hemos elegido 3 opciones para 2 de los 5 - 10 hiperparametros que tiene un random forest! Ni siquiera hemos empezado a hablar de otros modelos o ir más allá del modelo.

Si cada modelo tarda 10 segundos en entrenar, ya estaríamos hablando de 8 minutos de tiempo de entrenamiento - si quisiéramos mirar 3 opciones para otro hyperparameter estaríamos hablando de casi media hora.

#### Random search
Random search es similar, pero en vez de definir los valores exactos a explorar, definimos una distribución y el proceso elige combinaciones de forma "random".

Otras técnicas más avanzadas funcionan de forma similar, pero de alguna forma predicen que la combinación va a funcionar mejor y eligen algo random en esta zona.


#### ¿Qué pasa con todas las cosas que no son hiperparametros del modelo?
Hasta ahora no hemos mencionando 3 cosas importantes:

* Los diferentes modelos que tenemos disponibles
* Los pasos de preparación de datos
* Las variables que utilizamos en el modelo
  
##### Los pipelines y creatividad con los nombres
En realidad los 2 primeros puntos son fáciles de arreglar: simplemente incluirlos en el grid search. La manera de hacer esto en el código es utilizando los pipelines de sklearn y un poco de creatividad con el "grid" que definen. Aqui hay [un ejemplo](https://scikit-learn.org/stable/tutorial/statistical_inference/putting_together.html) pero los puntos importantes son:

* Definimos el grid para buscar con un diccionario O con un listado de diccionarios - cada diccionario define un conjunto de opciones para probar
* Cada paso en un pipeline tiene un nombre y podemos especificar las opciones para cada paso utilizado nombres especiales: `NombreDelPaso__NombreDelHiperparametro`
* Siempre podemos dar como opciones varios modelos / funciones a probar en cada paso, o [definir varios diccionarios](https://stackoverflow.com/a/50266037) donde cada diccionario especifica un modelo y un conjunto de opciones para este modelo

De esta forma podemos probar todos los conjuntos de pasos de preparación, modelos e hiperparametros que queramos!

##### Buscando las mejores variables
Para las variables el proceso es un poco más artístico. [Aquí](https://scikit-learn.org/stable/modules/feature_selection.html) tenemos varias opciones pero otra vez los procesos giran en torno a entrenar diferentes modelos con las variables disponibles y elegir el mejor.

## Estrategia

1. Definir bien las opciones que queremos explorar
2. Crear el "espacio" de búsqueda para nuestras funciones automatizadas
3. Ejecutar y buscar las mejores opciones

En realidad este tema es sobre todo un ejercicio de programación. Una vez tengamos nuestro código bien hecho, ejecutamos y esperamos a que termine. Para ahorrar tiempo, también es útil probar unas pocas opciones al principio e ir profundizando en los valores que mejor pinta tienen.

## Preguntas importantes para guiar

* ¿Cómo funcionan los pipelines y cómo puedo construir un proceso entero con pipelines?
* ¿Cuáles son los hiperparametros importantes para mis modelos?
* ¿Cuáles son las mejores funciones de sklearn para ayudarme?

## Que esperamos tener?
Un modelo "final" optimizado.

## Ejemplos para arrancar motores

### Un grid search basico

```python

grid = {
    'n_estimators' : [100, 500, 1000],
    'max_depth' : [None, 5, 10]
}

optimized_pipeline = sklearn.model_selection.GridSearchCV(sklearn.ensemble.RandomForestClassifier(random_state=0), grid)

optimized_pipeline.fit(train[X], train[target])

print(optimized_pipeline.best_params_)

probability = optimized_pipeline.predict_proba(test[X])[:,1]
```