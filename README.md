# Imbanaco-Proyecto :blue_book:

### **Contexto** 

En este proyecto que ira enfocado a una base de datos de la Clinica Imbanaco ubicada en la ciudad de Cali-Colombia analisamos y observamos diferentes equipos que adquierieron desde el año 1994 hasta el 2018.

### Datos que encontraremos en la base de datos
-  **Activo fijo**:  Numero que le otorga la institucion al equipo.
- **Serial** : Numero que identifica al equipo.
-  **Estado**:  Muestra si el equipo esta activo, depreciado, retirado o pendiente.
- **Costo**: Valor al momento de la adquisión del equipo.
- **Saldo**: Valor de la deuda que se debe del equipo.
- **Descripción** : Nombre del equipo.
- **Descripción técnica** : Lo que contiene el equipo.
- **Fecha**: Indicación del dia, mes y año de la obetención del equipo.
- **Desc. C. Costo**: Descripción de la ubicación del equipo.
- **Razon social del provedor**: Banco con el cual realizaron la compra y deben dinero.

#### Descripcion del proyecto
Para este proyecto se realizaron los siguientes planteamientos:
- **Limpieza de datos** : Identificación y manejo de los valores nulos o duplicados en el conjunto de datos. Tambien se realizara correnciones en los datos inconsistentes o erroneos.
- **Visualizacion de los datos** : Utilización de matplotlib y seaborn para la visualizacion de graficos, además para asi explorar patrones, tendencias y relaciones entre los datos.
- **Analisis exploratorio de los datos (EDA)** : Calculo de estadisticas descriptivas para comprender mejor la distribución de los datos, complementando asi un analisis exploratorio entre las diferentes variables.
- **Implementacion en MySQL**: Transferencia del dataframe de Pandas a una base de datos en MySQL, usando la conexion desde python

- **(No se realizaron imputaciones de los datos)**

## Desarrollo
El proyecto se enfoca principalmente en la base de datos de MODIFICADA1994 en la cual se observan equipos que llevan tiempo con un saldo que no ah cubierto la institución, por ende se realiza el analisis y la organización de los datos para que esta se ponga al dia con las deudas de sus equipos.

**Antes de empezar con el desarrollo por favor installar el archivo MODIFICADA1994 que sera el archivo con el cual vamos a trabajar**:exclamation: :heavy_exclamation_mark:

**Cabe aclarar que este trabajo se realizo en COLBORATORY de google y para que la archivo pueda ser leido en el COLAB primero se debe agregar al mismo**

1. Descargamos el archivo MODIFICADA1994.

![Descarga_captura](https://github.com/Ragnar0905/Imbanaco-Proyecto/assets/132869848/eb5897e0-7a77-4a60-ab7a-f36c20e63fd8)

2. Cargamos archivo.

![Seleccion_carpeta_COLABpng](https://github.com/Ragnar0905/Imbanaco-Proyecto/assets/132869848/6d177d1b-3e4d-430f-a7b6-de1e085a7d3a)

3. Cargamos el archivo MODIFICADA1994.xlsx en el COLAB

![Cargamos_archivo](https://github.com/Ragnar0905/Imbanaco-Proyecto/assets/132869848/8a677ea7-c172-479b-87e3-45d99318ea86)

#### Importacion de librerias

Importaremos librerias como seran la de pandas, numpy, matplotlib y seaborn
````python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
````
#### Manipulación de la base de datos

Al importar nuestras librerias empezaremos a manipular nuestro archivo MODIFICADA1994.xlsx
````python
data = pd.read_excel('MODIFICADA1994.xlsx') #Cargaremos el archivo a data
print(data) #Visualizaremos los datos de ese archivo
````
Luego para observar con que tipo de datos estaremos usando usamos la funcion de pandas .info()
````python
print(data.info()) #Esto desglosara una tabla con los datos que tenemos y su correspondiente tipo de dato
````
| #  | Column  | Non-Null Count | Dtype |
| :------------ |:---------------:| -----:| -----:|
| 0      | Activo | 112244 non-null | object |
| 1     | Serial     | 112246 non-null| float64|
| 2 | Unamed: 2        |    193031 non-null | float64|
| 3     | Descripción | 93768 non-null | object |
| 4  | Descripción Tencnica     |   85281 non-null | object |
| 5 | Estado       |    86987 non-null | object |
| 6      | Fecha | 112244 non-null | object |
| 7     | Costo     |   86987 non-null | object |
| 8 | Saldo       |    86987 non-null | object |
| 9      | C. Costo | 86987 non-null | float64|
| 10     | Desc. C.Costo     |   86987 non-null | object|
| 11 | Razon Social provedor        |    69770 non-null | object|
| 12 | Periodos a depreciar PCGA        |    86987 non-null | float64|

Por otro lado si queremos ver los primeros 5 datos de esta base podemos usar la funcion de pandas que nos lo permite la cual es .head()

````python
data.head() #Esto desglosara los primero 5 datos de la base de datos
````

#### Limpieza de Datos

**(Antes de empezar con la limpieza es una buena costumbre de realizar una copia de nuestra base de datos)**
`````python
df=data.copy() #Funcion de pandas
`````
Al haber realizado la copia de nuestra base datos miraremos los duplicados que tiene solo la columna de nuestro serial. Asi este nos mostrara que filas estan con el mismo serial.
````python
df[df.duplicated(subset='Serial')] #Duplicados solo por serial
# Muestra las filas duplicadas
print("Filas duplicadas por Serial:")
print(df)
````
Luego realizaremos la eliminacion de esos seriales duplicados
````python
# Eliminación de datos duplicados
df.drop_duplicates(subset=['Serial'], inplace=True)
print("Número total de filas después de eliminar duplicados:", df.shape[0])
````
El print nos mostrara lo siguiente:
> Número total de filas después de eliminar duplicados: 108509

Al tener en cuenta los datos duplicados eliminados pasaremos a ver cuantos nulos tiene cada fila
````python
#Conteo datos nulos
datos_nulos = df.isnull().sum()
print(datos_nulos)
````
Esto sacara en consola lo siguiente:

> Activo                           1
>
>Serial                           1
>
>Unnamed: 2                       7
>
>Descripcion                  18190
>
>DESCRIPCION TECNICA          25970
>
>ESTADO                       24927
>
>Fecha                            1
>
>Costo                        24927
>
>SALDO                        24927
>
>C. Costo                     24927
>
>Desc. C.Costo                24927
>
>Razon social proveedor       41513
>
>Periodos a depreciar PCGA    24927
>
>dtype: int64

##### Analisis de la columnas
Luego observamos que muchas columnas tienen muchos datos nulos (NaN) para este analisis que queremos realizar eliminaremos las siguientes columnas Descripcion Tencina, Unamed: 2, Razon social proveedor y Periodos a depreciar PCGA ya que para el analisis que queremos realizar sus datos nos son irrelevantes 

````python
#eliminacion de las columnas
df.drop(columns=['DESCRIPCION TECNICA'], inplace=True)
df.drop(columns=['Unnamed: 2'], inplace=True) #Nos dimos cuenta que es el mismo que el serial
df.drop(columns=['Razon social proveedor', "Periodos a depreciar PCGA"], inplace=True)
````
Cuando eliminamos las columnas que no nos aportan ninguna informacion para nuestro analisis, empezaremos a usar las columnas Saldo y Costo para poder ver que valores tienen un valor de 0
###### *Analisis de Saldo y Costo*
````python
saldo_cero_count = (df['SALDO'] == '$ 0,00').sum()
print("Cantidad de datos en la columna 'SALDO' con valor $0,00:", saldo_cero_count)
len(df)
````
Al imprimir estos valores nos da el siguiente resultado

>Cantidad de datos en la columna 'SALDO' con valor $0,00: 65786

Con esto podemos ver que tiene un aproximado a la mitad de los datos no tienen un saldo

Luego realizamos lo mismo pero con el costo
````python
saldo_cero_count = (df['Costo'] == '$ 0,00').sum()
print("Cantidad de datos en la columna 'costo' con valor $0,00:", saldo_cero_count)
len(df)
````
Para asi el print() nos muestre como resultado lo siguiente

> Cantidad de datos en la columna 'costo' con valor $0,00: 12371

######  *Analisis de Estado*
Ahora observaremos la columna de ESTADO para analizar la informacion que nos brinda

*Observamos que estados son nulos*
````python
nulos_estado = df['ESTADO'].isnull().sum()
nulos_estado
````
*Observamos que datos en estado retirado hay*

````python
#Contar cuantos retirados hay
retirados=(df['ESTADO']=='Retirado').sum()
retirados
````

*Eliminamos datos nulos*

Esto nos lanzara la cantidad de datos que quedara la columna el estado

````pyhton
df = df.dropna(subset=['ESTADO'])
nulos_estado = df['ESTADO'].isnull().sum()
nulos_estado
len(df)
````

**Vamos a ver que datos hay en estado con el unique()**

````python
#cuantos tipos de estado hay
valores_estado = df['ESTADO'].unique()

# Mostrar los valores únicos
print("Valores únicos en la columna 'ESTADO':", valores_estado)
````
> Valores únicos en la columna 'ESTADO': ['Activo' 'Retirado' 'Depreciado' 'Pendiente']

*Miramos en cada estado que valores son diferentes de 0*

**Retirado**
```` python
# Vamos a comparar los equipos que estan retirados pero tienen un saldo por pagar
retirados_no_cero = df[(df['ESTADO'] == 'Retirado') & (df['SALDO'] != '$ 0,00')]

# Imprime el resultado
print("Cantidad de datos con estado 'Retirado' y saldo diferente de '$ 0,00':", len(retirados_no_cero))
````
>Cantidad de datos con estado 'Retirado' y saldo diferente de '$ 0,00': 0

**Activo**
````
# Vamos a comparar los equipos que estan Activo pero tienen un saldo por pagar
Activo_no_cero = df[(df['ESTADO'] == 'Activo') & (df['SALDO'] != '$ 0,00')]

# Imprime el resultado
print("Cantidad de datos con estado 'Activo' y saldo diferente de '$ 0,00':", len(Activo_no_cero))
````
>Cantidad de datos con estado 'Activo' y saldo diferente de '$ 0,00': 17796

**Depreciado**
````python
# Vamos a comparar los equipos que estan depreciado pero tienen un saldo por pagar
Despreciado_no_cero = df[(df['ESTADO'] == 'Depreciado') & (df['SALDO'] != '$ 0,00')]

# Imprime el resultado
print("Cantidad de datos con estado 'Despreciado' y saldo diferente de '$ 0,00':", len(Despreciado_no_cero))
````
>Cantidad de datos con estado 'Despreciado' y saldo diferente de '$ 0,00': 0

**Pendiente**
````
# Vamos a comparar los equipos que estan retirados pero tienen un saldo por pagar
Pendiente_no_cero = df[(df['ESTADO'] == 'Pendiente') & (df['SALDO'] != '$ 0,00')]

# Imprime el resultado
print("Cantidad de datos con estado 'Pendiente' y saldo diferente de '$ 0,00':", len(Pendiente_no_cero))
````
>Cantidad de datos con estado 'Pendiente' y saldo diferente de '$ 0,00': 0

### Visualizacion de la base de datos

````python
#eliminacion de las columnas
df.drop(columns=['DESCRIPCION TECNICA'], inplace=True)
df.drop(columns=['Unnamed: 2'], inplace=True) #Nos dimos cuenta que es el mismo que el serial
df.drop(columns=['Razon social proveedor', "Periodos a depreciar PCGA"], inplace=True)
````
