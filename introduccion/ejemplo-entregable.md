# Ejemplo de un entregable
Esto es un pseudo-ejemplo de cómo puede ser un entregable típico a este tipo de ejercicio.

Ten en cuenta que es un ejemplo de una versión limpia - es probable que vayamos a tener varios trabajos sucios y que vayamos a dar varias vueltas antes de llegar a una versión bonita.

## El ejemplo

### Un titulo
Hola y bienvenido a mi ejemplo. El objetivo del ejemplo es dar un ejemplo simple para inspirar. Vamos a dividirlo en varias secciones y guiarte por lo que puede ser interesante incluir.

#### TLDR (o resumen ejecutivo)
El ejemplo se compone por varias secciones que detallan los pasos más importantes en un proyecto reducido de data science / machine learning. Después de una breve introducción y TLDR empezamos con un análisis de los datos para verificar ciertos detalles y entenderlos mejor. Luego pasamos a analizar el target y los factores que pueden influir en la predicción. Tras estos pasos creamos los modelos e incluimos una evaluación de su rendimiento. Aquí también es interesante revisar las mejoras que podemos aplicar al modelo para mejorarlo, sin ir demasiado lejos. Siempre debemos tener en cuenta el contexto del problema!

#### Carga de librerías y datos
Empezamos haciendo las cosas básicas - porque si este paso no funciona o tenemos algo mal, todo lo siguiente va a estar mal también.

#### Análisis de integridad
Normalmente cuando tenemos unos datos esperamos ciertas cosas de estos datos. Puede ser que tenemos un contexto amplio de qué esperar o puede ser que simplemente tenemos que utilizar nuestro propio conocimiento. Por ejemplo, si tienes datos sobre compras - esperarias información sobre el valor de la compra y que dicho valor no sea negativo ni tampoco fuera de un rango razonable (venta de chuches por millones no tiene sentido). Otras cosas a tener en cuenta son el número de nulos y valores únicos.

Otro punto importante es entender la unidad "básica" de los datos. Si tenemos datos sobre tweets, esperamos que cada fila sea un tweet. Aseguramos que sea así y que no haya duplicados.

Esta parte es muy básica pero es fundamental para no cometer graves errores más adelante.

#### Análisis de los datos
Luego, también tenemos que entender los datos a un nivel más conceptual. Tenemos que poner los datos en su contexto y aprender sobre este contexto. Esto es importante para tomar las decisiones apropiadas más adelante y poder entregar los conocimientos que vamos ganando.

Es una parte muy amplia sin respuestas "correctas". Tienes que utilizar tu intuición para determinar lo que sería interesante entender mejor y profundizar ahí. Por ejemplo, en datos de compra puede ser interesante ver cuando se hicieron las compras, que clientes compran más, los precios medios... todo lo que nos ayude a entender el contexto del problema mejor. En el caso de los tweets, la persona que publica los tweets parece que puede ser relevante - entonces podríamos profundizar un poco en esta dirección.

#### Análisis de relevancia de variables
Para hacer la predicción tenemos que tener un target definido y debemos también utilizar las variables más relevantes. Tirar todas nuestras variables en un modelo a la vez es una buena forma de liarnos y tener problemas. 

El objetivo de esta parte es tener un conjunto de datos limpio para el modelaje - con un target bien definido y un conjunto de variables con poder predictivo alto.

Hay varias formas de analizar la relevancia de una variable - por ejemplo cogiendo la media de nuestro target por los distintos valores de nuestra variable.

#### Modelado
Ahora creamos nuestro modelo utilizando los datos. Suele ser buena idea empezar por algo simple e ir agregando complejidad. Esta sección puede ser más o menos simple dependiendo de lo difícil que es nuestro problema de resolver.

#### Evaluacion
Es fundamental que evaluemos los modelos que vamos creando. El objetivo es estimar lo buenos que van a ser en el mundo real y elegir el mejor. Contestar la pregunta "cuál es el mejor" a veces no es lo más obvio.

Aquí también puede que intentemos hacer unas mejoras en nuestro modelo considerando lo que vamos viendo en la evaluación.

#### Conclusion
Por último - contestamos la pregunta de forma directa basándose en la evaluación que hemos hecho. Lo que escribimos aquí se puede incluir en el resumen ejecutivo.

## FAQ

### ¿Qué debo incluir en el entregable final?
Debemos incluir todos los pasos que nos ayudaron a llegar a la solución final y cualquier trabajo que resultó en algo "interesante". Esto incluye:

* Los pasos básicos del problema
* Los análisis que hicimos para hacer nuestras decisiones más importantes
* La creación de nuestro modelo
* La evaluación del modelo

El entregable debe ser "completo" - es decir - yo debo poder ejecutar y entender TODO los que has hecho sin tu presencia. Está OK si quieres dividir el trabajo en diferentes ficheros (por ejemplo un script de análisis y un reporte final), pero no podemos hacer cosas como "voy a cargar el modelo que he creado pero no tengo el codigo" o "el código no funciona porque no he incluido alguna cosa...".

### ¿Cuánto detalle debe incluir?
El detalle necesario para dar "chicha" al trabajo sin hacer que sea pesado de leer. Por ejemplo - si haces un análisis que no llega a ningún sitio, puede ser muy interesante incluirlo si es un resultado que consideramos interesante. Si fue algo que probaste porque tenias curiosidad y pasión por experimentar - lo podemos comentar sin incluir, o incluirlo en un fichero aparte.

### Cual es el mejor formato para el entregable?
El mejor formato es el que hace que tu trabajo sea más fácil de entender. Mucha gente prefiere utilizar los notebooks, pero no es 100% necesario. También recomiendo entregar en un formato fácil de cargar (un PDF o HTML suelen ser las mejores opciones). Si entregas tu trabajo en un word y la persona que tiene que leerlo no tiene word, ¿mal vamos no?