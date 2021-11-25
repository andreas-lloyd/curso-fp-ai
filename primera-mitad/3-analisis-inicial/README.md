# Análisis inicial de los datos
Lo primero de todo es entender nuestros datos y los problemas que podemos encontrar.

## Objetivo
Sacar conclusiones sobre la naturaleza de los datos que nos ayudará en la preparación de los datos y entrenamiento de un modelo.

## Contexto
Ahora mismo no conocemos bien los datos. Para poder predecir la popularidad de un Tweet en el futuro, tendremos que hacer muchas decisiones relacionados con:

* la construcción de un target relevante
* las técnicas de modelaje que vamos a tomar
* la creación y preparación de variables útiles para un modelo

Es la hora de estudiar los datos para ir formando conclusiones a alto nivel que concretamos más adelante. Por ejemplo, el siguiente paso en el proyecto será elegir un target específico y después analizar los factores que son importantes para nuestro target. Tenemos que llegar a este punto conociendo los datos mejor!

En cualquier proyecto que trata de un ámbito poco explorado, es muy común empezar entregando un análisis general de la situación y estamos en este punto ahora.

## Estrategia

1. Tener una idea a alto nivel de como podría ser nuestro modelo
2. Entender qué conceptos de los datos pueden ser relevantes para nuestra idea
3. Investigar estos conceptos para refinar (o cambiar) nuestro concepto inicial

## Preguntas importantes para guiar

* Qué son los conceptos importantes en nuestro proyecto y cómo se reflejan en los datos?
* Qué es lo mínimo que necesitamos para poder construir un modelo?
* Qué aspectos de los datos son deseables / no deseables?
* Qué tipo de transformaciones (de los datos) vamos a tener que hacer?

## Que esperamos tener?
Una serie de conclusiones sobre los diferentes aspectos de los datos, especialmente los que son más relevantes para nuestra predicción al futuro. Ayuda pensar que nuestro "cliente" quiere saber más en general sobre su problema (no solo la entrega de un modelo) y vamos a entregar este conocimiento.

## Ejemplos para arrancar motores

### El número total de Tweets
Cuáles son los hábitos normales de nuestros tweeters?

```python
twitter_users = pd.read_csv(handles_file)

# Como estan los datos a nivel general?
print(twitter_users.tweets.describe())

# Depende de cuanto tiempo lleva en la plataforma?
twitter_users['num_days_created'] = (pd.to_datetime('2022-01-01') - pd.to_datetime(twitter_users.join_date)).dt.days


graph = pn.ggplot(twitter_users, pn.aes(x='num_days_created', y='tweets')) + pn.geom_line()
graph.draw();

print(twitter_users[['num_days_created', 'tweets']].corr())
```

### Seguidores o seguidos?
Parece de cierto sentido común que estos factores sean importantes. Comó se comportan entre ellos?

```python
twitter_users = pd.read_csv(handles_file)

# Como estan los datos a nivel general?
print(twitter_users[['following', 'followers']].describe(percentiles=[0.75, 0.9, 0.95, 0.99]))


# Como se relacionan?
graph = pn.ggplot(twitter_users, pn.aes(x='following', y='followers')) + pn.geom_line()
graph.draw();

# Y el ratio?
twitter_users['follower_following_ratio'] = twitter_users.followers / twitter_users.following
print(twitter_users.follower_following_ratio.describe())

graph = pn.ggplot(twitter_users, pn.aes(x='followers', y='follower_following_ratio')) + pn.geom_line()
graph.draw();
```

## Algunas pistas más

### Estructurando el análisis
Un aspecto muy difícil de este ejercicio es que es muy abierto y cuando empiezas, parece muy alto nivel. Cómo te organizas es muy importante para conseguir algo bueno, unas pistas:

* Estructura tu notebook con las preguntas que quieres contestar - crea varias secciones en tu notebook que tienen como título una pregunta, y intenta contestar esta pregunta
* Empieza por lo más básico - una vez tengas claro que "podría utilizar esto para un modelo simple" puedes ir añadiendo complejidad, pero lo importante es tener una primera versión del análisis por lo simple que pueda ser

### Hay más datos!
El otro fichero (`2021-08-11-2021-08-12-2021-08-19-tweets-data.csv`) contiene los tweets que serán fundamentales para la predicción.

```python
tweet_data = pd.read_csv(tweet_file)

print(tweet_data.head())

print(tweet_data.nlikes.describe(percentiles=[0.5, 0.6, 0.7, 0.8, 0.9]))
```

### Utilizar los group by
¿De donde son la mayoría de los usuarios? ¿Qué días de la semana tienen más tweets? ¿Qué hashtags se utilizan más? 

Preguntas de este estilo solo se pueden contestar tirando del `groupby`. En general agregar los datos también es muy útil para quitar el "ruido" de los datos, por ejemplo:

```python
twitter_users = pd.read_csv(handles_file)

# Como estan los datos a nivel general?
print(twitter_users.tweets.describe())

# Depende de cuanto tiempo lleva en la plataforma?
twitter_users['num_days_created'] = (pd.to_datetime('2022-01-01') - pd.to_datetime(twitter_users.join_date)).dt.days


graph = pn.ggplot(twitter_users, pn.aes(x='num_days_created', y='tweets')) + pn.geom_line()
graph.draw();

twitter_users['num_weeks_created'] = twitter_users.num_days_created // 7
graph_data = twitter_users.groupby('num_weeks_created').tweets.median().reset_index()

graph = pn.ggplot(graph_data, pn.aes(x='num_weeks_created', y='tweets')) + pn.geom_line() # + pn.xlim(0, 52)
graph.draw();
```

### Piensa en lo fundamental

* Conceptos que son importantes: la popularidad, los factores que pueden predecir la popularidad (piensa lógicamente - que influye sobre la popularidad?)
* Variables que pueden ser importantes: likes, replies, followers, following, si tiene videos, si tiene hashtags, día de la publicación...
* ¿Cuáles son los pasos básicos para preparar los datos? Podemos utilizar variables que tienen muchos outliers? Ahora es buen momento para ir adelantando sobre estas decisiones
