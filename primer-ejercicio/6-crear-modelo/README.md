# Crear el modelo
La creación de nuestro modelo es el penúltimo paso. Depende de todos los pasos anteriores y si los hemos hecho bien, puede ser algo muy simple.

## Por qué?
Para tener un modelo hay que crear un modelo.

## Técnicas
Solemos tirar de `scikit-learn` para la creación de modelos por su proceso estandarizado. En general no hay muchas diferencias entre los diferentes modelos (podemos intercambiar los modelos en el código para probar diferentes cosas).

## Ejemplos

```python
y_train = train[''] # Tu target aquí
X_train = train[['', '']] # Tus variables aquí

model = LinearRegression() # Elegir el modelo
model.fit(X_train, y_train) # Entrenar el modelo

y_test = test[''] # Tu target aquí
X_test = test[['', '']] # Tus variables aquí

predictions = model.predict(X_test)
```