# Limpieza datos
La limpieza de los datos es dejar los datos en un estado mejor para el modelado.

## Por qué?
Si tenemos problemas en los datos, estos problemas se van a trasladar al modelo. Más problemas significa peores resultados. Problemas típicos incluyen:

* Nulos
* Outliers
* Filas con significados diferentes
* Filas repetidas

Todos afectando a la calidad de los datos de formas distintas.

## Técnicas
Cada problema tiene sus propias técnicas, unos comentarios generales:

* Puedo simplemente borrar filas? Si y no - borrar filas tiene sentido si piensas que la fila no tiene sentido o es un error, pero:
  * Si tienes muchas filas con problemas, te vas a quedar sin datos
  * Los datos externos pueden llegar con problemas - estos datos no se pueden borrar!
* Hay veces cuando un nulo tiene un significado especial (por ejemplo: la edad del hijo mayor de una pareja sin hijos)
* Los outliers pueden causar graves problemas a los modelos aunque sean valores validos - a veces estos valores también son los más interesantes!
* Tener poca muestra de ciertos valores discretos también es problemático - podemos agrupar como "otros"
* Evalúa bien si una columna con muchos problemas es útil o no

## Ejemplos

```python
perc_99 = data.LotArea.percentile(0.99)
data['LotArea_clipped'] = data.LotArea.clip(upper=perc_99)

data.isna().sum()

data.GarageType.fillna('No garage')
```