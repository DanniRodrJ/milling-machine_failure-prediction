# Dataset Description 📃

Este conjunto de datos sintéticos está modelado a partir de una fresadora existente y consta de 10.000 puntos de datos almacenados como filas con 14 características en columnas:

| Columna |Descripción |
|--------------|--------------|
| ```UID```      | Identificador único que va de 1 a 10000      |
| ```product ID```      | Está compuesto por una letra y un número de serie específico de la variante. La letra representa la calidad del producto y puede ser L, M o H, que corresponden a baja, media y alta calidad respectivamente.    |
| ```type```    | It represents the quality of the milling machine, and the letters L, M and H have the meaning explained in the variable ```product ID```|
| ```air temperature [K]```      |   Se genera de manera aleatoria alrededor de una temperatura base de 300 K, utilizando un proceso en el que los cambios se ajustan dentro de una variación de 2 K.   |
| ```process temperature [K]```      | Generada de forma aleatoria siguiendo una distribución normalizada con una desviación estándar de 1 K. Luego, se suma a la temperatura del aire más 10 K.      |
| ```rotational speed [rpm]```      | Se calcula a partir de una potencia de 2860 W y se superpone con un ruido distribuido normalmente. Indica la velocidad de rotación de la fresadora en revoluciones por minuto (rpm).     |
| ```torque [Nm]```      | Los valores de torque siguen una distribución normal alrededor de 40 Nm, con una desviación estándar de 10 Nm y no se permiten valores negativos. El torque es una medida de la fuerza de torsión aplicada en la fresadora, y estos valores describen su variación en el conjunto de datos     |
| ```tool wear [min]```      | Esta columna indica el desgaste de la herramienta en minutos. Las variantes de calidad H/M/L agregan 5/3/2 minutos de desgaste a la herramienta utilizada en el proceso. Es decir, dependiendo de la calidad del producto, se suma una cantidad específica de tiempo de desgaste a la herramienta utilizada      |
| ```machine failure```      | Indica si la máquina ha fallado en un punto de datos particular y si alguno de los siguientes modos de falla es verdadero. La falla de la máquina puede ser causada por cinco modos de falla independientes      |
| ```TWF (tool wear failure)```      | La herramienta se reemplaza o falla en un momento de desgaste de herramienta seleccionado al azar entre 200 y 240 minutos. En el conjunto de datos, la herramienta se reemplaza 69 veces y falla 51 veces en este punto de tiempo (asignado aleatoriamente)     |
| ```HDF (heat dissipation failure)```      | El proceso falla si la diferencia entre la temperatura del aire y la temperatura del proceso es inferior a 8.6 K y la velocidad de rotación de la herramienta es inferior a 1380 rpm (144.5 rad/s). Esto ocurre en 115 puntos de datos      |
| ```PWF (power failure)```      | El producto del torque y la velocidad de rotación (en rad/s) representa la potencia requerida para el proceso. Si esta potencia está por debajo de 3500 W o por encima de 9000 W, el proceso falla, lo cual sucede 95 veces en el conjunto de datos    |
| ```OSF (overstrain failure)```      | Si el producto del desgaste de herramienta y el torque supera los valores de umbral (11000 minNm (0.18) para la variante L, 12000 minN para la variante M (0.20) y 13000 minNm (0.21) para la variante H), el proceso falla debido a una sobrecarga. Esto ocurre en 98 puntos de datos     |
| ```RNF (random failures)```      | Cada proceso tiene una probabilidad del 0.1% de fallar independientemente de sus parámetros de proceso. Esto ocurre solo en 5 puntos de datos, lo cual es menos de lo esperado para 10,000 puntos de datos en el conjunto de datos     |

Si al menos uno de los modos de falla anteriores es verdadero, el proceso falla y la etiqueta de ```machine failure``` (falla de la máquina) se establece en 1. Sin embargo, el modelo no puede especificar qué modo de falla concreto es responsable de esa falla.

Para que el modelo pueda predecir el tipo de falla específico, se necesitaría incluir características o atributos adicionales en el conjunto de datos que estén relacionados con cada modo de falla individual.

Para que el modelo pueda predecir el tipo de falla específico, se necesitaría incluir características o atributos adicionales al conjunto de datos que estén relacionados con cada modo de falla individual. Estos atributos podrían ser variables que indiquen las condiciones específicas en las que ocurre cada tipo de falla, como la temperatura, la velocidad de rotación, el desgaste de la herramienta o cualquier otra información relevante para cada modo de falla.

## Feature Engineer

| Columna |Descripción |
|--------------|--------------|
| ```Temp_difference [k]```      | Atributo que es la diferencia de temperaturas cae en el rango asociado con el modo de falla (HDF)      |
| ```power```| El producto del torque y la velocidad de rotación|

Es importante tener en cuenta que estas inferencias o estimaciones estarían basadas en relaciones y suposiciones y no en información explícita sobre el tipo de falla. Por lo tanto, los resultados pueden ser aproximados y estar sujetos a cierta incertidumbre.
