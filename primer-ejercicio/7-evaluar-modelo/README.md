# Evaluar modelo
El proceso de crear un modelo termina con la evaluación del modelo.

## Por qué?
Tenemos que poder confiar en nuestro modelo para poder utilizarlo. Utilizamos la evaluación para ganar esta confianza.

## Técnicas
Ahora no vamos a profundizar mucho en las técnicas de evaluación, que son muy amplias. Por ahora destacamos que:

* Evaluamos utilizando métricas de evaluación, que suelen representar la diferencia entre el target real y las predicciones del modelo
* Evaluamos principalmente utilizando el conjunto de test
* Siempre es buena idea reflexionar sobre los resultados y traerlo al mundo real - un cliente o compañero no va a entender si el valor de una métrica especifica es buena o no
  * De hecho, es difícil para nosotros saber si un resultado es bueno o no - lo más habitual es comparar resultados de diferentes modelos (incluyendo el caso cuando NO usamos un modelo)

Nota: normalmente procedemos a iterar nuestro modelo tras la evaluación - mejorandolo poco a poco - pero está prohibido mirar los resultados de test y luego pretender que podemos volver a usar este conjunto para evaluar nuestros modelos "mejorados". Los datos de test deben simular datos "no vistos" y en el momento que los usamos para crear el modelo, ya se han visto. Por esto es común utilizar otro conjunto de datos - los de validación - para mejorar el modelo.

## Ejemplos
Las métricas más comunes para la regresión se pueden encontrar [aquí](https://scikit-learn.org/stable/modules/model_evaluation.html).

```python
from sklearn.metrics import median_absolute_error

test['baseline'] = test['SalePrice'].mean()

print(median_absolute_error(test['SalePrice'], test['baseline']))
print(median_absolute_error(test['SalePrice'], predictions))
```