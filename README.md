# Taller #1
Se presentan los resultados del Taller #1 del curso de Introducción a la Ciencia de Datos.

## Pregunta a Responder
**Existe una diferencia significativa entre el salario promedio de un egresado de Ingeniería Mecánica e Ingeniería Electrónica en Colombia? Si es así, es posible realizar una predicción de los mismos utilizando un modelo generado a partir de los datos?**

## Datos Utilizados
<!--- Los datos utilizados fueron obtenidos a partir del **SNIES** (Sistema Nacional de Información de la Educación Superior), el cuál es una rama del Ministerio de Educación Colombiano. --->

Los datos, ya limpios, consisten de 3 columnas: titulo obtenido, salario mensual (en pesos colombianos) y tiempo de experiencia (en meses). Un extracto ejemplo de los datos se presenta a continuación:
| Titulo | Salario | Experiencia |
| :---: | :---: | :---: |
| Ingeniería Mecánica | $ 4.054.403 | 34 |
| Ingeniería Mecánica | $ 5.370.630 | 60 |
| Ingeniería Electrónica | $ 4.188.643 | 42 |
| Ingeniería Mecánica | $ 5.678.137 | 60 |
| Ingeniería Electrónica | $ 3.821.573 | 39 |
| Ingeniería Electrónica | $ 3.564.493 | 28 |

## Procedimiento
Ya teniendo los datos limpios, se procedió a realizar gráficas de la suma acumulada del salario en ambos casos. Así, se obtuvo la siguiente gráfica:

<p align="center">
  <img src="https://github.com/dfdiazc/IntroCienciaDatos1/blob/main/results/cumulative_distribution.png?raw=true">
</p>

Igualmente, se obtuvo un valor para la diferencia entre las medias de ambas distribuciones, obteniendo el valor (en millones de pesos) de:

```python
real_diff = np.mean(salary_mechanical) - np.mean(salary_electronic)
real_diff = 0.21866747928436947
```

Ahora, ya teniendo este dato, se plantea la hipótesis nula, es decir, el hecho de que ambos datos (las medias de ambas distribuciones) provengan de la misma distribución de datos. Para realizar la prueba de hipótesis, se utilizó la técnica de Shuffle, realizando 10000 iteraciones y obteniendo la diferencia entre las medias en cada una de éstas. Así, se obtuvo la siguiente gráfica:

<p align="center">
  <img src="https://github.com/dfdiazc/IntroCienciaDatos1/blob/main/results/mean_diff_distribution.png?raw=true">
</p>

En ésta se muestra tanto la distribución obtenida como el valor de "real_diff" calculado anteriormente. Así, se calculó ahora el valor de p-value correspondiente, obteniendo el valor de:

```python
p_value = np.count_nonzero(diffs > real_diff)/len(diffs)
p_value = 0.0212
```

Es decir, comparando este resultado con un valor estándar de 0.05, vemos que es posible negar la hipótesis nula, respondiendo así a la primera parte de la pregunta planteada. Esto es, la diferencia entre el salario promedio entre las dos profesiones es estadísticamente significativa.

Ahora, habiendo respondido esto, queremos encontrar un modelo para hacer predicciones con respecto a los salarios. Así, se utilizó ahora la técnica de Bootstrapping para realizar una regresión lineal. En ambos casos, se obtuvo la distribución correspondiente para los parámetros de los ajustes lineales: la pendiente, el intercepto y el valor de R-cuadrado. Así, se realizaron 10000 iteraciones y se obtuvieron las siguientes gráficas:

<p align="center">
  <img src="https://github.com/dfdiazc/IntroCienciaDatos1/blob/main/results/linear_regression_mechanical.png?raw=true"><img src="https://github.com/dfdiazc/IntroCienciaDatos1/blob/main/results/linear_regression_electronic.png?raw=true">
</p>

En rojo se muestra la recta obtenida para el valor medio de tanto la pendiente como el intercepto, mientras que, en gris, se muestran todas las otras rectas obtenidas para la distribución de parámetros. Asimismo, se muestran los datos originales sobre la regresión.

Tal como se mencionó anteriormente, se obtuvieron las diferentes distribuciones para cada uno de los parámetros del ajuste lineal en cada caso, lo que se ilustra a continuación:

<p align="center">
  <img src="https://github.com/dfdiazc/IntroCienciaDatos1/blob/main/results/linear_distributions_mechanical.png?raw=true"><img src="https://github.com/dfdiazc/IntroCienciaDatos1/blob/main/results/linear_distributions_electronic.png?raw=true">
</p>

En cada gráfica se muestra el valor medio para cada una de las distribuciones. De estos cabe destacar los valores de R-cuadrado obtenidos. En ambos casos, este valor es bastante cercano a 1, indicando una muy buena correlación lineal entre los datos, es decir, éstos se ajustan de buena manejar a una regresión lineal.

Ya teniendo estos datos, es posible realizar predicciones utilizando los modelos obtenidos. Así, se obtuvieron las siguientes predicciones para salarios de 6, 7, 8, 9 y 10 años de experiencia para cada carrera, ilustradas en la siguiente gráfica:

<p align="center">
  <img src="https://github.com/dfdiazc/IntroCienciaDatos1/blob/main/results/predictions.png?raw=true">
</p>

## Resultados
Como resultado es posible decir que fue posible responder satisfactoriamente a la pregunta planteada inicialmente. Sí hay una diferencia significativa entre los salarios promedio de un egresado de Ingeniería Mecánica y uno de Ingeniería Electrónica, pudiendo realizar predicciones a partir de los modelos obtenidos utilizando técnicas estadísticas, las que se resumen a continuación:
| Experiencia | Ingeniería Mecánica | Ingeniería Electrónica |
| :---: | :---: | :---: |
| 6 | $ 6.100.207 +/- 0.040075 | 6.010.203 +/- 0.052622 |
| 7 | $ 6.838.023 +/- 0.051945 | 6.804.926 +/- 0.070780 |
| 8 | $ 7.575.839 +/- 0.064053 | 7.599.649 +/- 0.089303 |
| 9 | $ 8.313.656 +/- 0.076287 | 8.394.372 +/- 0.108002 |
| 10| $ 9.051.472 +/- 0.088594 | 9.189.096 +/- 0.126801 |

Así, utilizando los datos obtenidos, se concluye que, en promedio, en Colombia, un egresado de Ingeniería Mecánica tiene un salario de $ 218.667 mayor que uno de Ingeniería Electrónica, teniendo en cuenta los años de experiencia en ambas carreras.
