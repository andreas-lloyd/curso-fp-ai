# Relevancia variables
La relevancia de una variable es su influencia sobre nuestro target. Más relevante significa que seguramente tendrá más impacto en el modelo final.

## Por qué?
En general menos variables en un modelo final significa un modelo con menos poder, pero más robusto. Si nos quedamos con solo las variables más relevantes, retenemos el máximo de poder con el máximo de simplicidad.

## Técnicas

* Correlación entre variables continuas
* Medias del target por grupos de una variable discreta
* Creación de modelos con distintas variables
* Importancia de variables (arboles de decision) y otras técnicas de "información"

Es habitual repetir estos análisis por las diferentes variables de interés. También hay que tener en cuenta que variables poco relevantes pueden aportar una información única que otras no aportan - por esto es importante ver la correlación entre las variables en si.

## Ejemplos

```python
data[['LotArea', 'SalePrice']].corr()

data.groupby('SaleCondition').SalePrice.describe()
data.groupby('SaleCondition').LotArea.describe()
```