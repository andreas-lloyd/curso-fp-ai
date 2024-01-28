# Predecir popularidad
## TLDR

1. Predecir popularidad de Tweets
2. Crear modelos de **clasificación** - NO regresión
3. Más foco en la creación de modelos, evaluación y optimización
4. Ahora no hay preguntas para guiar el ejercicio, pero el concepto es lo mismo y la entrega debe ser parecida (cubrir los mismos puntos)

## Objetivo
Vamos a imaginar que trabajamos para una empresa que quiere crecer su base de usuarios. Imaginamos también que hemos identificado Twitter como una posible fuente de usuarios nuevos.

Hemos visto que la clave es la creación de contenidos buenos (no spam!) y compartirlo sobre tweets populares cuando antes después de la publicación del tweet. Por ejemplo, si Obama habla sobre cómo el deporte afecta al desarrollo de los niños - escribir y compartir un artículo que profundiza sobre este tema en los comentarios podría traernos muchos usuarios.

Ahí la empresa nos ha pedido ayuda - cómo podemos predecir los tweets que van a ser populares (en el momento que se publiquen)? 

Entonces nuestro trabajo es poder proporcionar inteligencia (de alguna forma) sobre qué tweets podrán llegar a ser “populares” y válidos para nuestra estrategia.

## Puntos prácticos

### Modelos de clasificación
Ahora queremos centrarnos en clasificación - esto significa que

* Queremos predecir un target DISCRETO y no continuo (tiene un número de valores finitos)
* Entrenaremos con modelos de clasificación
* Las perdiciones y evaluaciones que haremos son diferentes al anterior ejercicio

### Los datos

* Datos de tweets y información sobre los usuarios (2 conjuntos)
* Todos los usuarios son relativamente "populares" (para evitar montones de tweets irrelevantes)
* No tenemos ningún target creado de forma artificial - lo tendréis que definir vosotros

### Foco de aprendizaje
Ahora que entendemos mejor los básicos - vamos a centrarnos en los puntos un poco más avanzados

* Entrenamiento y comparación de diferentes modelos
* Evaluación más profunda de las predicciones
* Métodos de optimización automatizados

### Formato
El formato del ejercicio y su entrega es muy similar al ejercicio de antes, salvo que ahora no vamos a tener preguntas para guiarnos. De todas formas, la metodología sigue siendo la misma y debéis estructurar el trabajo de una forma similar.