# Targets para clasificación
La clasificación se hace un un target <discreto> - una variable con un número de valores distintos finitos. El ejemplo más común es un target binario - solo 2 valores.

Tenemos que crear un target que representa la popularidad de nuestros tweets

* Tenemos que elegir una variable o combinación de variables que formaran la base de nuestro target - acuérdate de que la calidad del dato es muy importante para nuestro target
* Luego tenemos que definir exactamente como convertirlo en algo discreto
* Puede ser una buena idea probar diferentes variables para nuestro target

## Ejemplo con código
Buscamos popularidad - al fin y al cabo no nos importa tanto si un tweet tiene 10 o 20 likes, pero 10 o 10,000.

```python
print(tweets_data.nlikes.quantile([0.5, 0.8, 0.9, 0.95]))
tweet_data['muchos_likes'] = tweet_data.nlikes >= tweets_data.nlikes.quantile(0.9)

print(tweet_data.groupby('muchos_likes').nlikes.describe())