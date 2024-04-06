# Imbanaco-Proyecto 🏥📘

### **Contexto** 

Este proyecto esta enfocado en el analisis de la base de datos de equipos que adquierieron desde el año 1994 hasta el año 2018 en la Clinica Imbanaco ubicada en la ciudad de Cali (Colombia).

### ⚠️*Problemática*⚠️
La Clínica Imbanaco cuenta con una base de datos donde registran los equipos adquiridos, se requiere analizarla y organizarla para determinar cuales de 
ellos tienen saldo pendiente de pago para ponerse al día.

### 🔍Datos que encontraremos en el repositorio🔍
‼️**NOTA: El codigo de la limpieza, visualizacion y manejo de MySQL se encontraran en proyectoAlmacenamiento.ipynb**‼️

- Excel de la base de datos Modificada1994 (ANTES DE LA LIMPIEZA)
- Codigo en lenguaje python para la limpieza y visualizacion de los datos **(Formato .ipynb)**
- Codigo en lenguaje python para manejo de MySQL **(Formato .ipynb)**
- Base de datos df_final.csv (DESPUES DE LA LIMPIEZA)

*Datos que encontraremos en el excel de MODIFICADA1994*

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

*Tipos de datos que se encontrara en MODIFICADA1994*

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

#### 👨‍🏫Descripcion del proyecto👨‍🏫
Para este proyecto se realizaron los siguientes planteamientos:
- **Limpieza de datos** : Identificación y manejo de los valores nulos o duplicados en el conjunto de datos. Tambien se realizara correnciones en los datos inconsistentes o erroneos.
- **Visualizacion de los datos** : Utilización de matplotlib y seaborn para la visualizacion de graficos, además para asi explorar patrones, tendencias y relaciones entre los datos.
- **Implementacion en MySQL**: Transferencia del dataframe de Pandas a una base de datos en MySQL, usando la conexion desde python

- **(No se realizaron imputaciones de los datos)**

## ✍️Desarrollo✍️

**Antes de empezar con el desarrollo por favor installar el archivo MODIFICADA1994 que sera el archivo con el cual vamos a trabajar**:exclamation: :heavy_exclamation_mark:

**Cabe aclarar que este trabajo se realizo en COLBORATORY de google y para que la archivo pueda ser leido en el COLAB primero se debe agregar al mismo**

1. Descargamos el archivo MODIFICADA1994.

![Descarga_captura](https://github.com/Ragnar0905/Imbanaco-Proyecto/assets/132869848/eb5897e0-7a77-4a60-ab7a-f36c20e63fd8)

2. Cargamos archivo.

![Seleccion_carpeta_COLABpng](https://github.com/Ragnar0905/Imbanaco-Proyecto/assets/132869848/6d177d1b-3e4d-430f-a7b6-de1e085a7d3a)

3. Cargamos el archivo MODIFICADA1994.xlsx en el COLAB

![Cargamos_archivo](https://github.com/Ragnar0905/Imbanaco-Proyecto/assets/132869848/8a677ea7-c172-479b-87e3-45d99318ea86)

#### 📖Importacion de librerias📖

Librerias que deberias tener en cuanta como pandas, numpy, matplotlib y seaborn
````python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
````
