# Train y test
La división entre train y test es la separación de los datos para el entrenamiento.

## Por qué?
Esta división es fundamental para la correcta evaluación de nuestro modelo. Lo utilizamos para simular la llegada de "nuevos" datos - lo que pasa cuando nuestro modelo vive en el mundo real.

## Técnicas

* Separación random - un porcentaje de los datos en train y un porcentaje en test
* Separar por fechas - elegimos una fecha a partir de la cual todos los datos son de "test"

## Ejemplos

```python
from sklearn.model_selection import train_test_split

train, test = train_test_split(data, test_size=0.3, random_state=1)
```