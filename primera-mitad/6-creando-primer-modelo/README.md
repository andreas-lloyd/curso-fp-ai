# Creando nuestro primero modelo
Vamos a progresar y crear nuestra primera regresion.

## Objetivo
Crear un modelo que predice la popularidad de un tweet y sacar las predicciones.

## Contexto
Hemos progresado mucho:

* Entendemos nuestro data set
* Sabemos que variables representan la popularidad y conocemos los problemas que vamos a encontrar
* Tenemos claro que variables son potenciales predictores de nuestro target

Ahora toca lo que hemos venido aqui para hacer: entrenar un modelo. Lo que siempre hay que tener claro en nuestras cabezas es que el modelo final es solo 50% del "entregable" a nuestro cliente - la otra parte es la evaluacion de como va a hacer su trabajo este modelo. No comprarias un coche sin hacer un test drive y ver opiniones primero verdad?

Esta parte del proyecto se puede hacer en 5 lineas o en 500, con 2 variables o 100, entrenando 1 modelo o 5 - lo fundamental es que seguimos un proceso correcto que va a permitir una evaluacion a posterior que tenga sentido. Si no tenemos claro mas o menos como de bueno va a ser nuestro modelo con datos nuevos, no contara para nada nuestro esfuerzo.

Esta parte es tan vinculado con la parte de evaluacion que es probable que ya adelantemos parte de la evaluacion (el ultimo paso) para hacer esta parte mejor.

## Estrategia
Ahora las cosas son un poco mas simples y roboticos - ya hemos hecho lo dificil en las partes anteriores.

1. Tener claro que variables de entrada y el target que queremos para el modelo
2. Construir los pasos de preparacion de datos para que nuestro modelo se puede entrenar (y de la mejor forma)
3. Entrenar nuestro modelo y predecir con ello

Podemos repetir estos pasos varias veces con diferentes combinaciones - de hecho - esto es lo mas habitual.

## Preguntas importantes para guiar

* Que son los requisitos basicos para las variables de entrada al modelo? Como puede entrenar sin que me de error? (haz lo minimo primero!)
* Que son los otros pasos de preparacion de datos que pueden mejorar el resultado?
* Como se entrenan modelos con scikit-learn? (usar otras librerias si querais!)
* Como puedo guardar un modelo ya entrenado?
* Como se puede sacar predicciones de mis modelos?
* Que son los pasos **muy importantes** para asegurar una evaluacion posterior buena? ([hint](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html))

## Que esperamos tener?
Unas predicciones que podemos evaluar en la siguente parte. Necesitamos por lo menos predicciones de un modelo - pero seria interesante tener varios para comparar. Crear un nuevo modelo puede ser tan simple como modificar las variables de entrada.

## Ejemplos para arrancar motores
