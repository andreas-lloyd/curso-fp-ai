# Carga de datos
La carga de datos es la importación de los datos en nuestro espacio de trabajo.

## Por qué?
El origen, almacenaje, análisis y ejecución de modelos suelen hacerse en lugares distintos. La carga correcto de los datos de su ubicación de almacenaje es importante para poder proceder con el análisis.

## Técnicas

* Ficheros tipo CSV: cargamos ficheros con datos desde una ubicación local o remota (más común en el mundo de tutoriales)
* Leer directamente de una base de datos (más común en el mundo real)
* Siempre tenemos que comprobar que los datos se han cargado de forma correcta y que sean  relevantes para nuestro problema
  * Numero de filas correcto
  * Cada fila representa algo único y lo esperado
  * No tener nulos donde no los esperamos

## Ejemplos
```python
data = pd.read_csv(data_file)

data.head()
data.shape
data.nunique()
data.info()
data.describe()
```