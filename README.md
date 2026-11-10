# Data_analysis
Data Analysis https://formacion.thebridge.tech/ 

![Data Science con IA](https://raw.githubusercontent.com/aupatxus/ONLINE_DS_THEBRIDGE_GitHub/refs/heads/main/Vital%20LANBIDE.png)






# NumPy y Matrices en Python

## Introducción a NumPy

**NumPy (Numerical Python) es la librería fundamental en Python para la computación científica y el análisis de datos.** 

Su principal ventaja radica en la introducción de los **arrays** (`ndarray`), estructuras de datos homogéneas y optimizadas que permiten almacenar y procesar colecciones de elementos de forma extremadamente rápida y eficiente, superando por mucho el rendimiento de las listas nativas de Python.


---

## 1. Listas vs. Matrices y Arrays

### Listas nativas de Python
* **Flexibilidad extrema:** Pueden almacenar cualquier tipo de datos de forma combinada (números, strings, booleanos, objetos).
* **Inadecuadas para cálculo matemático estructurado:** Esa misma flexibilidad las vuelve lentas e ineficientes al procesar grandes volúmenes de datos numéricos.
* **Representación de matrices básicas:** Se logran mediante "listas de listas" (ej. `[[1, 2], [3, 4]]`), pero operar matemáticamente con ellas exige bucles `for` anidados, lo cual resulta tedioso y de bajo rendimiento.

### Arrays de NumPy (`ndarray`)
* **Homogeneidad estricta:** Todos los elementos dentro del array deben ser obligatoriamente del mismo tipo de dato.
* **Eficiencia en memoria:** Almacenados en bloques de memoria contiguos, lo que permite la **vectorización** (aplicar operaciones matemáticas a miles de datos simultáneamente sin usar bucles `for`).

---

## 2. Configuración e Instalación

Para instalar NumPy en tu entorno de desarrollo local, ejecuta el siguiente comando en la terminal:

````
pip install numpy
````

Para comenzar a utilizarlo en tus scripts de Python, debes importarlo bajo el alias estándar de la comunidad:

````
import numpy as np
````

---

## 3. Creación de Arrays

Existen diferentes funciones integradas para inicializar arrays dependiendo de las necesidades del desarrollo:

* **Desde colecciones de Python:**
  ````
  vector = np.array([1, 2, 3])                 # Array de 1 Dimensión
  matriz = np.array([[1, 2], [3, 4]])          # Array de 2 Dimensiones (Matriz)
  ````
* **Con valores predefinidos:**
  ````
  ceros = np.zeros((3, 4))                     # Matriz de 3x4 rellena de 0.0
  unos = np.ones((2, 2))                       # Matriz de 2x2 rellena de 1.0
  vacia = np.full((2, 3), 7)                   # Matriz de 2x3 llena con el número 7
  ````
* **Mediante secuencias numéricas:**
  ````
  rango = np.arange(0, 10, 2)                  # Genera de 0 a 9 saltando de 2 en 2 -> [0, 2, 4, 6, 8]
  lineal = np.linspace(0, 1, 5)                # 5 números equiespaciados entre 0 y 1 -> [0. , 0.25, 0.5 , 0.75, 1.]
  ````
* **Con números aleatorios:**
  ````
  aleatorio = np.random.rand(3, 3)             # Matriz 3x3 con decimales aleatorios entre 0 y 1
  ````

---

## 4. Atributos del Array

Cada objeto array contiene propiedades nativas que permiten inspeccionar su estructura física en cualquier momento (nota que se accede a ellos sin usar paréntesis):

* **`ndim`:** Indica el número total de dimensiones o ejes (un vector tiene 1, una tabla o matriz tiene 2).
* **`shape`:** Devuelve una tupla que detalla el tamaño de cada dimensión en el formato `(filas, columnas)`.
* **`size`:** Indica la cantidad total de elementos individuales que contiene el array.
* **`dtype`:** Muestra el tipo de dato asignado a los elementos internos.

````
mi_matriz = np.array([[1, 2, 3], [4, 5, 6]])
print(mi_matriz.ndim)   # Resultado: 2
print(mi_matriz.shape)  # Resultado: (2, 3) -> 2 filas y 3 columnas
print(mi_matriz.size)   # Resultado: 6
````

---

## 5. Indexado y Slicing (Rebanado)

### Indexado (Selección Única)
Sirve para extraer o modificar un único elemento. Al igual que en Python elemental, el conteo de posiciones empieza en `0`.
* **En arrays 1D (Vectores):** Funciona igual que en las listas ordinarias: `array[posicion]`.
* **En arrays 2D (Matrices):** Se utiliza la sintaxis **`[fila, columna]`**.

````
matriz = np.array([[10, 20], [30, 40]])
print(matriz[0, 1])  # Fila 0, Columna 1 -> 20
print(matriz[1, 0])  # Fila 1, Columna 0 -> 30
````

### Slicing (Extracción de Subarrays)
Permite cortar fragmentos del array usando la notación matemática estándar `[inicio:fin:paso]`. Cuando trabajamos en dos dimensiones, los cortes de filas y columnas se separan mediante una coma: **`[filas_inicio:filas_fin, columnas_inicio:columnas_fin]`**.

````
matriz = np.array([[1, 2, 3], , 
                   [7, 8, 9]])

# Extraer las primeras dos filas y las dos primeras columnas
sub_matriz = matriz[0:2, 0:2]  # Resultado: [[1, 2], [4, 5]]

# Extraer una fila completa usando el operador ':'
primera_fila = matriz[0, :]    # Resultado: [1, 2, 3]
````

---

## 6. Reshape (Cambio de Forma)

El método **`.reshape()`** modifica la disposición de filas y columnas de un array sin alterar sus datos internos. 

* **Regla de oro:** El número total de elementos (`size`) del array original y del nuevo array transformado debe ser estrictamente idéntico.

````
vector = np.array([1, 2, 3, 4, 5, 6])  # Tamaño original: 6
matriz_nueva = vector.reshape((2, 3))  # Transforma a 2 filas y 3 columnas

print(matriz_nueva)
# Resultado:
# [[1, 2, 3],
#]
````

---

## 7. Tipos de Datos (Dtypes)

NumPy requiere homogeneidad para optimizar el uso de memoria RAM y el caché de la CPU. Los tipos de datos nativos más habituales son `int32`, `int64`, `float64` y `bool`.

Puedes forzar el tipo de dato al momento de inicializar el array o convertir uno ya existente mediante el método **`.astype()`**:

````
# Forzar tipo flotante (decimal) en la creación
enteros_a_float = np.array([1, 2, 3], dtype='float64')  # Resultado: [1., 2., 3.]

# Convertir un array existente truncando los decimales (sin redondear)
decimales = np.array([1.9, 2.5, 3.1])
enteros_nuevos = decimales.astype('int32')              # Resultado: [1, 2, 3]
````

---

## 8. Concatenación y Splitting

### Concatenación (Unión)
Unir dos o más arrays se realiza a través de la función `np.concatenate()`. En espacios bidimensionales, es obligatorio determinar el eje de unión (`axis`):
* **`axis=0`:** Unión vertical (añade filas hacia abajo).
* **`axis=1`:** Unión horizontal (añade columnas hacia los lados).

````
a = np.array([[1, 2]])
b = np.array([[3, 4]])

vertical = np.concatenate([a, b], axis=0)    # Resultado: [[1, 2], [3, 4]]
horizontal = np.concatenate([a, b], axis=1)  # Resultado: [[1, 2, 3, 4]]
````

### Splitting (División)
Es la operación inversa a la concatenación y fragmenta un único array en múltiples secciones más pequeñas mediante las utilidades `np.split()`, `np.vsplit()` (corte vertical) o `np.hsplit()` (corte horizontal).

````
datos = np.array([10, 20, 30, 40, 50, 60])
# Divide el array en los índices de corte 2 y 4
parte1, parte2, parte3 = np.split(datos, [2, 4])

print(parte1)  # Resultado: [10, 20]
print(parte2)  # Resultado: [30, 40]
print(parte3)  # Resultado: [50, 60]
````

---

## 9. Sustitución y Copias en Memoria

### Sustitución Directa y Filtrado Booleano
Modificar datos es un proceso directo asignando nuevos valores a las coordenadas o subarrays seleccionados. Es muy común el **filtrado booleano** para aplicar cambios masivos basados en una condición lógica:

````
x = np.array([10, 20, 30])
x[1] = 99  # Reemplaza el valor en el índice 1 -> [10, 99, 30]

# Sustitución condicional masiva
edades = np.array([15, 25, 12, 40])
edades[edades < 18] = 0  # Convierte cualquier número menor de 18 en 0 -> [0, 25, 0, 40]
````

### El peligro de las "Vistas" vs `.copy()`
⚠️ **¡Atención!** En NumPy, cuando realizas un corte o *slicing* numérico (ej. `sub = matriz[0:2]`), **no estás creando un objeto nuevo**, sino una "vista" orientada al bloque de memoria original. Si modificas `sub`, la matriz de origen cambiará también.

Si necesitas un fragmento completamente independiente que no afecte al objeto raíz, debes clonarlo explícitamente con **`.copy()`**:

````
original = np.array([1, 2, 3])

# Clonación real e independiente en memoria
copia_segura = original.copy()
copia_segura[0] = 99 

print(original)      # Resultado: [1, 2, 3] (Se mantiene intacto)
print(copia_segura)  # Resultado: [99, 2, 3]
````

---

## 10. Agregaciones y Estadísticas

NumPy incorpora funciones matemáticas sumamente veloces capaces de procesar estructuras de datos enteras o colapsar información en torno a un eje estadístico determinado:

* **`np.sum()`**: Sumatoria de los elementos.
* **`np.min() / np.max()`**: Encuentra los valores mínimos y máximos.
* **`np.mean()`**: Calcula la media (promedio).
* **`np.std()`**: Calcula la desviación estándar.
Puedes aplicarlos a todo el array o a un eje específico (por ejemplo, calcular la suma solo de cada columna usando axis=0).
````
numeros = np.array([[1, 2], [3, 4]])

print(np.sum(numeros))          # 10 (Suma total)
print(np.mean(numeros, axis=0)) # [2. , 3.] (Media de cada columna)
````






<hr>








# PANDAS

https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf

---

## 1. El Concepto de Tidy Data (Datos Limpios)

Un conjunto de datos se considera **Tidy (ordenado/limpio)** si actúa como base para la manipulación y cumple con dos principios:
* **Columnas:** Cada variable se almacena en su propia columna.
* **Filas:** Cada observación se guarda en su propia fila.

Este formato complementa de forma ideal las operaciones vectorizadas de pandas, garantizando que se preserven las observaciones automáticamente a medida que manipulas las variables. Ningún otro formato funciona de manera tan intuitiva.

---

## 2. Creación de DataFrames

Existen diferentes formas de especificar valores al inicializar un objeto `DataFrame`:

* **Especificando valores por columnas (Diccionario):**
````
    df = pd.DataFrame(
        {"a" :, 
         "b" :, 
         "c" : [10, 11, 12]}, 
        index =)
````
* **Especificando valores por filas (Lista de listas):**
````
    df = pd.DataFrame(
        [[4, 7, 10],
,
         [6, 9, 12]], 
        index=[1, 2, 3], 
        columns=['a', 'b', 'c'])
````
* **Con índice multinivel (MultiIndex):**
````
    df = pd.DataFrame(
        {"a" : [4 ,5, 6], 
         "b" :, 
         "c" : [10, 11, 12]}, 
        index = pd.MultiIndex.from_tuples(
            [('d', 1), ('d', 2), ('e', 2)], 
            names=['n', 'v']))
````
---

## 3. Remodelado de Datos (Reshaping Data)

Funciones clave para cambiar el diseño (*layout*), ordenamiento, reindexación y renombrado de las tablas:

* **`pd.melt(df)`**: Reúne columnas y las convierte en filas (*Gather columns into rows*).
* **`df.pivot(columns='var', values='val')`**: Distribuye los valores de las filas y los convierte en columnas (*Spread rows into columns*).
* **`pd.concat([df1, df2])`**: Concatena o añade las filas de los DataFrames.
* **`pd.concat([df1, df2], axis=1)`**: Concatena o añade las columnas de los DataFrames.
* **`df.sort_values('mpg')`**: Ordena las filas según los valores de una columna de menor a mayor (bajo a alto).
* **`df.sort_values('mpg', ascending=False)`**: Ordena las filas de mayor a menor (alto a bajo).
* **`df.rename(columns={'y': 'year'})`**: Renombra las columnas de un DataFrame.
* **`df.sort_index()`**: Ordena el DataFrame de acuerdo con sus índices.
* **`df.reset_index()`**: Restablece el índice a números secuenciales de fila y mueve el índice anterior a las columnas.
* **`df.drop(columns=['Length', 'Height'])`**: Elimina o descarta las columnas especificadas del DataFrame.

---

## 4. Filtrado y Selección de Subconjuntos (Subsetting)

Permite seleccionar filas individuales, columnas o una combinación de ambas utilizando los indexadores nativos de pandas.

### Filtrado de Observaciones (Subconjunto de Filas)
* **`df[df.Length > 7]`**: Extrae las filas que cumplen un criterio lógico determinado.
* **`df.drop_duplicates()`**: Remueve las filas duplicadas (solo tiene en cuenta el valor de las columnas).
* **`df.sample(frac=0.5)`**: Selecciona aleatoriamente una fracción (porcentaje) de las filas totales.
* **`df.sample(n=10)`**: Selecciona aleatoriamente una cantidad fija `n` de filas.
* **`df.nlargest(n, 'value')`**: Selecciona y ordena las `n` entradas con los valores más altos (*top*).
* **`df.nsmallest(n, 'value')`**: Selecciona y ordena las `n` entradas con los valores más bajos (*bottom*).
* **`df.head(n)`**: Selecciona las primeras `n` filas.
* **`df.tail(n)`**: Selecciona las últimas `n` filas.
* **`df.query('Condición')`**: Permite usar expresiones booleanas en forma de cadena de texto para filtrar filas.
    * *Ejemplo:* `df.query('Length > 7')`
    * *Ejemplo con AND:* `df.query('Length > 7 and Width < 8')`
    * *Ejemplo con texto:* `df.query('Name.str.startswith("abc")', engine="python")`

### Selección de Variables (Subconjunto de Columnas)
* **`df[['width', 'length', 'species']]`**: Selecciona múltiples columnas mediante una lista con nombres específicos.
* **`df['width']` o `df.width`**: Selecciona una única columna por su nombre.
* **`df.filter(regex='regex')`**: Selecciona las columnas cuyos nombres coincidan con la expresión regular `regex`.

### Subconjuntos combinados (Filas y Columnas de forma simultánea)
*El primer índice selecciona las filas y el segundo índice selecciona las columnas.*
* **`df.iloc[10:20]`**: Selecciona las filas en las posiciones numéricas desde la 10 hasta la 20.
* **`df.iloc[:, [1, 2, 5]]`**: Selecciona todas las filas, pero únicamente las columnas en las posiciones 1, 2 y 5 (la primera columna es la 0).
* **`df.loc[:, 'x2':'x4']`**: Selecciona todas las filas y todas las columnas ubicadas en el rango comprendido entre las etiquetas 'x2' y 'x4' (inclusive).
* **`df.loc[df['a'] > 10, ['a', 'c']]`**: Selecciona las filas que cumplen la condición lógica y recupera únicamente las columnas específicas declaradas.
* **`df.iat[1, 2]`**: Accede a un único valor rápido en la tabla por su posición/índice numérico de fila (1) y columna (2).
* **`df.at[4, 'A']`**: Accede a un único valor por medio de sus etiquetas de fila (4) y columna ('A').

---

## 5. Cadenas de Métodos (Method Chaining)

Dado que la gran mayoría de los métodos de pandas devuelven un nuevo objeto `DataFrame`, es posible aplicar otro método inmediatamente sobre el resultado. Esta práctica optimiza y mejora drásticamente la legibilidad del código al modelar un flujo de trabajo estructurado:
````
    df = (pd.melt(df)
          .rename(columns={'variable': 'var', 'value': 'val'})
          .query('val >= 200'))
````
---

## 6. Operadores Lógicos y Expresiones Regulares

### Lógica en Python y Pandas
* `<` / `>` : Menor que / Mayor que.
* `==` / `!=` : Igual a / No igual a.
* `<=` / `>=` : Menor o igual que / Mayor o igual que.
* `df.column.isin(values)` : Comprobación de pertenencia a un grupo (Group membership).
* `pd.isnull(obj)` : Identifica si el objeto es un valor nulo o `NaN`.
* `pd.notnull(obj)` : Identifica si el objeto NO es nulo.
* `&`, `|`, `~`, `^`, `df.any()`, `df.all()` : Operadores lógicos elementales Y (*and*), O (*or*), NO (*not*), XOR, o validaciones globales.

### Ejemplos de Expresiones Regulares (Regex)
* `'\.'` : Coincide con cadenas que contengan un punto físico `.`.
* `'Length$'` : Coincide con cadenas que terminen exactamente con la palabra 'Length'.
* `'^Sepal'` : Coincide con cadenas que comiencen con la palabra 'Sepal'.
* `'^x[1-5]$'` : Coincide con cadenas que incien con 'x' y terminen con un dígito del 1 al 5.
* `'^(?!Species$).*'` : Coincide con cualquier cadena excepto la palabra exacta 'Species'.

---

## 7. Creación de Nuevas Columnas y Funciones Vectorizadas

Pandas expone un amplio abanico de funciones vectorizadas que operan eficientemente sobre columnas enteras o sobre un elemento individual (`Series`).

* **`df.assign(Area=lambda df: df.Length * df.Height)`**: Calcula y añade una o más columnas nuevas al vuelo, devolviendo un nuevo DataFrame.
* **`df['Volume'] = df.Length * df.Height * df.Depth`**: Añade directamente una nueva columna asignando los valores de forma directa.
* **`pd.qcut(df.col, n, labels=False)`**: Divide o segmenta una columna en `n` contenedores (*buckets*) balanceados cuantitativamente.

### Funciones Vectorizadas Adicionales
* **`max(axis=1)`** : Encuentra el valor máximo de forma horizontal (elemento por elemento en la fila).
* **`min(axis=1)`** : Encuentra el valor mínimo de forma horizontal por fila.
* **`clip(lower=-10, upper=10)`** : Recorta los valores numéricos para mantenerlos dentro de los umbrales límite definidos.
* **`abs()`** : Calcula el valor absoluto de los elementos.

---

## 8. Tratamiento de Datos Faltantes (Handling Missing Data)

* **`df.dropna()`**: Elimina todas las filas que contengan datos nulos (`NA`/`null`) en cualquiera de sus columnas.
* **`df.fillna(value)`**: Reemplaza la totalidad de los datos nulos (`NA`/`null`) presentes en la estructura con el valor indicado.

---

## 9. Agrupación y Ventanas de Datos (Group Data & Windows)

### Agrupar Datos (`groupby`)
* **`df.groupby(by="col")`**: Devuelve un objeto de tipo `GroupBy` agrupado por los valores de la columna llamada `"col"`.
* **`df.groupby(level="ind")`**: Devuelve un objeto de tipo `GroupBy` agrupado por los valores del nivel de índice llamado `"ind"`.


### Funciones Adicionales de GroupBy
Los ejemplos de funciones vectorizadas también pueden aplicarse a grupos. En este caso, la función se aplica grupo por grupo y los vectores devueltos tienen la longitud del DataFrame original:
* **`size()`**: Devuelve el tamaño o cantidad de elementos de cada grupo.
* **`agg(function)`**: Agrega el grupo aplicando una función específica.

### Cálculos en Ventanas (Windows)
* **`df.expanding()`**: Devuelve un objeto de tipo `Expanding` que permite aplicar funciones de resumen de forma acumulativa.
* **`df.rolling(n)`**: Devuelve un objeto de tipo `Rolling` que permite aplicar funciones de resumen a ventanas deslizantes de longitud `n`.

---

## 10. Resumen Estadístico y Agregaciones (Summarize Data)

Pandas proporciona un amplio conjunto de funciones de resumen que operan sobre diferentes tipos de objetos de pandas (columnas de DataFrame, `Series`, `GroupBy`, `Expanding` y `Rolling`) y producen valores únicos para cada uno de los grupos. Cuando se aplican a un DataFrame, el resultado se devuelve como una `Series` de pandas para cada columna.

### Funciones Estadísticas y de Resumen
* **`df['w'].value_counts()`**: Cuenta el número de filas con cada valor único de la variable.
* **`len(df)`**: Indica el número de filas en el DataFrame.
* **`df.shape`**: Devuelve una tupla con el número de filas y el número de columnas del DataFrame.
* **`df['w'].nunique()`**: Indica el número de valores distintos o únicos en una columna.
* **`df.describe()`**: Genera estadísticas descriptivas básicas para cada columna (o GroupBy).
* **`df.info()`**: Imprime un resumen conciso del DataFrame.
* **`df.memory_usage()`**: Imprime el uso de memoria de cada columna en el DataFrame.
* **`df.dtypes`**: Imprime una Serie con el tipo de dato (`dtype`) de cada columna en el DataFrame.
* **`sum()`**: Suma los valores de cada objeto.
* **`count()`**: Cuenta los valores no nulos (`non-NA/null`) de cada objeto.
* **`median()`**: Calcula el valor de la mediana de cada objeto.
* **`quantile([0.25,0.75])`**: Calcula los cuantiles de cada objeto.
* **`apply(function)`**: Aplica una función a cada objeto.
* **`min()`**: Obtiene el valor mínimo en cada objeto.
* **`max()`**: Obtiene el valor máximo en cada objeto.
* **`mean()`**: Calcula el valor medio o promedio de cada objeto.
* **`var()`**: Calcula la varianza de cada objeto.
* **`std()`**: Calcula la desviación estándar de cada objeto.

---

## 11. Combinación de Conjuntos de Datos (Combine Data Sets)

### Cruces Estándar (Standard Joins)
Permiten unir filas coincidentes entre dos DataFrames (`adf` y `bdf`) basándose en una columna común (`on='x1'`):

* **`pd.merge(adf, bdf, how='left', on='x1')`**: Une las filas coincidentes de `bdf` a `adf`. Conserva todas las filas de `adf`.
* **`pd.merge(adf, bdf, how='right', on='x1')`**: Une las filas coincidentes de `adf` a `bdf`. Conserva todas las filas de `bdf`.
* **`pd.merge(adf, bdf, how='inner', on='x1')`**: Une los datos. Retiene únicamente las filas presentes en ambos conjuntos de datos.
* **`pd.merge(adf, bdf, how='outer', on='x1')`**: Une los datos. Retiene todos los valores y todas las filas de ambos conjuntos.

### Cruces de Filtrado (Filtering Joins)
* **`adf[adf.x1.isin(bdf.x1)]`**: Selecciona todas las filas en `adf` que tienen una coincidencia en `bdf`.
* **`adf[~adf.x1.isin(bdf.x1)]`**: Selecciona todas las filas en `adf` que NO tienen una coincidencia en `bdf`.

### Operaciones de Tipo Conjunto (Set-like Operations)
Operaciones para comparar o combinar DataFrames (`ydf` y `zdf`) con las mismas columnas:
* **`pd.merge(ydf, zdf)`**: Intersección. Devuelve las filas que aparecen tanto en `ydf` como en `zdf`.
* **`pd.merge(ydf, zdf, how='outer')`**: Unión. Devuelve las filas que aparecen en cualquiera o en ambos DataFrames.
* **Diferencia de Conjuntos (*Setdiff*):** Para obtener las filas que aparecen en `ydf` pero no en `zdf`:
````
    (pd.merge(ydf, zdf, how='outer', indicator=True)
     .query('_merge == "left_only"')
     .drop(columns=['_merge']))
````

### Funciones de Clasificación y Desplazamiento
* **`shift(1)`**: Copia la estructura con los valores desplazados (retardados) en 1 posición.
* **`shift(-1)`**: Copia la estructura con los valores adelantados en 1 posición.
* **`cumsum()`**: Suma acumulativa.
* **`cummax()`**: Valor máximo acumulativo.
* **`cummin()`**: Valor mínimo acumulativo.
* **`cumprod()`**: Producto acumulativo.
* **`rank(method='dense')`**: Asigna rangos consecutivos sin dejar huecos en la numeración.
* **`rank(method='min')`**: Asigna rangos de clasificación. Los empates obtienen el rango mínimo del grupo.
* **`rank(pct=True)`**: Asigna rangos reescalados al intervalo continuo.
* **`rank(method='first')`**: Asigna rangos de clasificación. Los empates se asignan según el primer valor encontrado.

---

## 12. Operaciones Especiales (Cambio de Tipo, Texto y Fechas)

### Cambio de Tipo (Changing Type)
* **`pd.to_numeric(data)`**: Convierte tipos de datos no numéricos a tipo numérico.
* **`pd.to_datetime(data)`**: Convierte tipos de datos no temporales al tipo `datetime`.
* **`pd.to_timedelta(data)`**: Convierte tipos de datos no temporales al tipo `timedelta`.
* **`df.astype(type)`**: Convierte los datos a casi cualquier tipo dado, incluyendo el tipo categórico (`categorical`).
* **`df.infer_objects()`**: Intenta inferir un mejor tipo de dato para las columnas con tipo de dato genérico `object`.
* **`df.convert_dtypes()`**: Convierte las columnas a los mejores tipos de datos posibles sugeridos nativamente por pandas.

### Operaciones de Cadenas en Series (Series String Operations)
Operaciones vectorizadas que se aplican a una serie completa utilizando el accesor `str`:
* **`s.str.count(pattern)`**: Devuelve una serie con los conteos enteros del patrón en cada elemento.
* **`s.str.get(index)`**: Devuelve una serie con el elemento extraído en el índice indicado para cada posición.
* **`s.str.join(sep)`**: Devuelve una serie donde cada elemento ha sido concatenado usando el separador indicado.
* **`s.str.title()`**: Convierte el primer carácter de cada palabra en mayúscula.
* **`s.str.len()`**: Devuelve una serie con la longitud de cada elemento.
* **`s.str.cat()`**: Concatena los elementos individuales en una única cadena global.
* **`s.str.partition(sep)`**: Divide la cadena tomando la primera instancia del separador especificado.
* **`s.str.slice(start, stop, step)`**: Extrae un fragmento indexado de cada cadena de la serie.
* **`s.str.replace(pat, rep)`**: Usa expresiones regulares para reemplazar patrones en cada una de las cadenas.
* **`s.str.isalnum()`**: Comprueba si cada uno de los elementos de la serie es de tipo alfanumérico.

### Fechas y Horas (Datetime)
Con una Serie que contiene datos de tipo `datetime`, el accesor `dt` se utiliza para obtener varios componentes de los valores temporales:
* **`s.dt.year`**: Extrae el componente del año de la fecha.
* **`s.dt.month`**: Extrae el mes como un número entero.
* **`s.dt.day`**: Extrae el número de día de la fecha.
* **`s.dt.quarter`**: Identifica en qué trimestre del año se encuentra la fecha.
* **`s.dt.hour`**: Extrae la hora.
* **`s.dt.minute`**: Extrae el minuto.
* **`s.dt.second`**: Extrae el segundo.

### Mapeos y Transformaciones (Mapping)
Permiten aplicar un mapeo a cada elemento de un DataFrame o Serie, lo cual resulta útil para recategorizar o transformar los datos:
* **`s.map(lambda x: 2*x)`**: Devuelve una copia de la serie donde cada entrada se duplica.
* **`df.apply(lambda s: s.max() - s.min(), axis=1)`**: Devuelve una Serie con la diferencia entre los valores máximos y mínimos de cada fila del DataFrame (`axis=1`).

---

## 13. Visualización de Datos (Plotting)

Métodos directos de pandas para graficar rápidamente la información contenida en los DataFrames de forma nativa:

* **`df.plot()`**: Traza un gráfico de líneas estándar para el DataFrame.
* **`df.plot.scatter(x='w', y='h')`**: Traza un gráfico de dispersión (scatter plot).
* **`df.plot.hist()`**: Traza un histograma de frecuencias.
* **`df.plot.pie()`**: Traza un gráfico de pastel.
* **`df.plot.bar()`**: Traza un gráfico de barras.
* **`df.plot.boxplot()`**: Traza un gráfico de caja y bigotes.
* **`df.plot.area()`**: Traza un gráfico de área.
* **`df.plot.hexbin()`**: Traza un gráfico de densidad con contenedores hexagonales.

### Argumentos y Combinaciones de Gráficos
* **`subplots=True`**: Separa la información en gráficos independientes para cada columna del DataFrame.
* **`title="Texto"`**: Define el título o la lista de títulos de las gráficas (ej. `df.plot(subplots=True, title=['col1', 'col2', 'col3'])`).
* **`stacked=True`**: Apila los datos de las columnas uno encima del otro (aplica solo para los tipos de gráficos `bar`, `barh` y `area`).
* **`alpha=0.5`**: Establece la transparencia de la representación visual al 50%.
* **`cumulative=True`**: Crea un gráfico de carácter acumulativo.
* **`bins=30`**: Establece el número de contenedores (*bins*) en los que se agrupan los datos para los histogramas.

---

## 14. Entrada y Salida de Archivos (Input/Output)

Los tipos de archivo comunes para la entrada de datos incluyen CSV, JSON y HTML, los cuales son legibles por humanos, mientras que los tipos de salida comunes suelen estar más optimizados para el rendimiento y la escalabilidad, tales como Feather, Parquet y HDF.

### Lectura de datos (Input)
* **`df = pd.read_csv(filepath)`**: Lee datos estructurados desde un archivo CSV.
* **`df = pd.read_html(filepath)`**: Lee datos en formato de tabla desde un archivo HTML.
* **`df = pd.read_excel(filepath)`**: Lee datos desde archivos Excel (.xls y relacionados).
* **`df = pd.read_sql(filepath)`**: Lee el resultado de una consulta o tabla desde una base de datos SQL.
* **`pd.read_clipboard()`**: Lee texto plano copiado directamente desde el portapapeles del sistema.

### Escritura y Exportación (Output)
* **`df.to_parquet(filepath)`**: Escribe los datos del DataFrame a un archivo en formato binario Parquet.
* **`df.to_feather(filepath)`**: Escribe los datos del DataFrame a un archivo en formato binario Feather.
* **`df.to_hdf(filepath)`**: Escribe los datos a un archivo jerárquico HDF.
* **`df.to_clipboard()`**: Copia el objeto de pandas directamente en el portapapeles del sistema de la máquina.

---

## 15. Configuraciones y Opciones Globales

Pandas ofrece algunas "opciones" globales para controlar el comportamiento general de la librería, el despliegue estético de la información en pantalla, entre otros. Las opciones pueden ser consultadas y modificadas directamente a través de la sintaxis orientada a objetos: `pd.options.option_name` (donde `option_name` es el nombre específico de la opción).
* *Ejemplo de uso:* `pd.options.display.max_rows = 20` (Establece el número máximo de filas mostradas a 20).

### Funciones de Control de Opciones
* **`get_option(option)`**: Recupera el valor actual asignado a la opción especificada.
* **`set_option(option)`**: Asigna un nuevo valor para la opción indicada.
* **`reset_option(options)`**: Restablece los valores de todas las opciones indicadas a sus configuraciones originales por defecto.
* **`describe_option(options)`**: Imprime en la consola las descripciones técnicas completas de las opciones solicitadas.
* **`option_context(options)`**: Ejecuta un bloque de código bajo configuraciones temporales de opciones que vuelven automáticamente a sus valores previos tras completar la ejecución.

### Opciones de Visualización (*Display options*) Comunes
* **`display.max_rows`**: El número máximo de filas desplegadas cuando se formatea un DataFrame en texto legible (*pretty-print*).
* **`display.max_columns`**: El número máximo de columnas desplegadas de forma formateada en la pantalla.
* **`display.expand_frame_repr`**: Controla si la representación visual del DataFrame se distribuye o estira a través de múltiples páginas.
* **`display.large_repr`**: Controla si un DataFrame que supera los límites máximos establecidos de filas o columnas se trunca por completo o se resume de forma compacta.
* **`display.precision`**: Establece la precisión de salida en posiciones decimales para los números de punto flotante.
* **`display.max_colwidth`**: El ancho máximo permitido para las columnas; las celdas cuyos caracteres superen esta medida serán truncadas de forma automática.
* **`display.max_info_columns`**: El número máximo de columnas a mostrar detalladamente tras invocar de forma explícita el método estructural `info()`.
* **`display.chop_threshold`**: Establece el umbral de redondeo automático a cero cuando se despliega una Serie o DataFrame con valores numéricos insignificantes.
* **`display.colheader_justify`**: Controla cómo se alinean y justifican los textos correspondientes a los encabezados de las columnas.







<hr>





# Introducción a Pandas

**Pandas es una librería de Python orientada a la manipulación y análisis de datos**. En un nivel básico, sus objetos fundamentales pueden ser considerados como versiones mejoradas de los arrays estructurados de NumPy, diferenciándose principalmente en que las filas y columnas se identifican mediante etiquetas explícitas en lugar de simples índices enteros.

---

## 1. Estructuras de Datos Fundamentales

Pandas se basa en tres estructuras de datos esenciales: la `Serie` (unidimensional), el `DataFrame` (bidimensional) y el `Index`.

### El Objeto Serie de Pandas
Una `Serie` es un array unidimensional de datos indexados. Envuelve una secuencia de valores (que son un array de NumPy accesible mediante `.values`) y una secuencia de índices (accesible mediante `.index`).

*   **Diferencia con NumPy:** Mientras que un array de NumPy tiene un índice entero implícito, una `Serie` tiene un índice definido explícitamente asociado a los valores.
*   **Flexibilidad del Índice:** El índice explícito no necesita ser un entero; puede contener cadenas de texto (por ejemplo, nombres de estados o personas), IDs numéricos no contiguos o no secuenciales.
*   **Analogía con Diccionarios:** Puede verse como una especialización de un diccionario de Python. Un diccionario mapea claves arbitrarias a valores arbitrarios, mientras que una `Serie` asigna claves tipificadas a valores tipificados. Esta tipificación interna la hace mucho más eficiente que los diccionarios de Python para operaciones de datos.

### El Objeto Pandas DataFrame
Un `DataFrame` representa una estructura de datos bidimensional con etiquetas en filas y columnas. Puede interpretarse desde dos perspectivas:

1.  **Como Matriz Generalizada de NumPy:** Es el análogo a un array bidimensional con índices de fila y nombres de columna flexibles. También puede definirse como una secuencia ordenada de objetos `Series` alineados que comparten el mismo índice.
2.  **Como Diccionario Especializado:** Mapea un nombre de columna a una `Serie` de datos de columna. 

*   *Punto de confusión común:* En un array bidimensional de NumPy, `data[0]` devuelve la primera *fila*. En un `DataFrame` de Pandas, `data['col0']` devuelve la primera *columna*.

### El Objeto Index de Pandas
Tanto las `Series` como los `DataFrames` contienen un índice explícito accesible mediante el atributo `.index`. El `Index` puede considerarse como un *array inmutable* o como un *conjunto ordenado* (multiconjunto, ya que permite valores repetidos).

*   **Inmutabilidad:** Los objetos `Index` no pueden ser modificados por medios normales (ej. `ind[1] = 0` arroja un `TypeError`). Esto garantiza que sea seguro compartir índices entre múltiples `DataFrames` y arrays sin riesgo de modificaciones colaterales inadvertidas.

---

## 2. Construcción de Objetos

### Creación de Series (`pd.Series(data, index=index)`)
El argumento `data` puede ser una de las siguientes entidades:
*   **Una lista o array de NumPy:** El índice por defecto será una secuencia de enteros.
*   **Un escalar:** El valor se repite para llenar el índice explícito especificado (ej. `pd.Series(5, index=[100, 200, 300])`).
*   **Un diccionario:** El índice toma por defecto las claves del diccionario (ej. `pd.Series({2:'a', 1:'b', 3:'c'})`). Si se pasa un `index` explícito junto al diccionario, la serie se rellenará únicamente con las claves identificadas explícitamente.

### Creación de DataFrames
Se pueden construir de múltiples maneras:
*   **A partir de un único objeto Serie:** Genera un DataFrame de una sola columna.
*   **A partir de una lista de diccionarios:** Cada diccionario representa una fila. Si faltan claves en algunos diccionarios, Pandas rellena automáticamente esos huecos con valores nulos `NaN`.
*   **A partir de un diccionario de objetos Serie:** Donde las claves del diccionario se convierten en los nombres de las columnas.
*   **A partir de un array bidimensional de NumPy:** Permite especificar una lista de nombres de columnas (`columns`) y de filas (`index`). Si se omiten, se usan índices enteros secuenciales.
*   **A partir de un array estructurado de NumPy:** Convierte de forma directa los campos del array estructurado en columnas.

---

## 3. Indexación, Selección y Modificación de Datos

Pandas hereda los patrones de selección de NumPy (slicing, máscaras booleanas, fancy indexing) pero añade particularidades debido a la coexistencia de índices explícitos e implícitos.

### Selección en Series
*   **Slicing por Índice Explícito:** Al utilizar etiquetas (ej. `data['a':'c']`), el elemento final del rango **se incluye** en el resultado.
*   **Slicing por Índice Implícito:** Al utilizar posiciones enteras estilo Python (ej. `data[0:2]`), el elemento final del rango **se excluye**.
*   **Modificación:** Es posible ampliar o modificar una serie usando asignación directa de estilo diccionario (ej. `data['e'] = 1.25`).

### Indexadores Especiales (`loc` e `iloc`)
Para evitar confusiones e imprecisiones (especialmente cuando el índice explícito está compuesto por números enteros), Pandas proporciona indexadores específicos:
*   **`.loc`:** Realiza búsquedas y cortes haciendo referencia estrictamente al **índice explícito** (etiquetas).
*   **`.iloc`:** Realiza búsquedas y cortes haciendo referencia estrictamente al **índice implícito posicional** de estilo Python (enteros de `0` a `longitud-1`).

### Selección en DataFrames
*   **Estilo Diccionario:** Acceso a columnas individuales mediante su nombre (ej. `data['area']`). También es posible el acceso estilo atributo (ej. `data.area`), excepto si el nombre de la columna es numérico o entra en conflicto con un método integrado del DataFrame (por ejemplo, el método `.pop()`).
*   **Añadir Columnas:** Permite insertar nuevas columnas calculadas de forma directa (ej. `data['density'] = data['pop'] / data['area']`).
*   **Transposición:** El atributo `.T` transpone el DataFrame completo, intercambiando filas por columnas.
*   **Slicing directo y Máscaras:** Por defecto, las operaciones de slicing directo (ej. `data[1:3]`) o máscaras booleanas (ej. `data[data.density > 100]`) aplicadas sin indexador operan sobre las **filas** y no sobre las columnas.
*   **Uso de `loc` e `iloc` bidimensionales:** Permiten seleccionar subconjuntos de filas y columnas al mismo tiempo usando la sintaxis `[filas, columnas]`:
    *   `data.iloc[:4, 1:3]` selecciona por posición las primeras 4 filas y las columnas en las posiciones 1 y 2.
    *   `data.loc[data.density > 100, ['pop', 'density']]` aplica una máscara booleana sobre las filas y selecciona columnas específicas por etiqueta.

---

## 4. Operaciones con Datos y Alineación de Índices

### Preservación de Índices con Ufuncs
Al aplicar cualquier función universal (ufunc) unaria de NumPy (como `np.exp()`, `np.sin()`, etc.) sobre un objeto de Pandas, la operación se ejecuta elemento a elemento y **se preservan intactas las etiquetas de los índices y columnas** en el objeto resultante.

### Alineación Automática de Índices
En operaciones binarias (como suma, resta o multiplicación entre dos objetos), Pandas **alinea automáticamente los índices** de ambos elementos.

*   **Unión de Índices:** El resultado de la operación contiene la *unión* de los índices de los objetos de entrada.
*   **Tratamiento de Datos Faltantes (`NaN`):** Si un elemento no coincide o no existe en uno de los dos objetos, Pandas le asigna el valor nulo `NaN` por defecto (ej. `A * B`).
*   **Métodos con valores de relleno (`fill_value`):** Para evitar la propagación de valores `NaN`, se pueden usar métodos explícitos de Pandas en lugar de los operadores aritméticos estándar de Python. Pasar el argumento `fill_value` permite sustituir los valores faltantes por un valor numérico específico antes de realizar la operación:
    *   `A.add(B, fill_value=0)`

### Operaciones entre DataFrames y Series
Las operaciones entre un `DataFrame` (2D) y una `Serie` (1D) siguen reglas de difusión (broadcasting) similares a las de NumPy.

*   **Comportamiento por defecto:** Las operaciones aritméticas directas (ej. `df - df.iloc[0]`) alinean la `Serie` con las **columnas** del `DataFrame`, repitiendo la operación en cada fila.
*   **Operaciones por Filas:** Si se requiere aplicar la operación a lo largo de las columnas (alineando la `Serie` con el índice de filas), se deben utilizar los métodos explícitos de Pandas especificando el argumento `axis=0`:
    *   `df.subtract(df['R'], axis=0)`
*   Si las columnas o índices no coinciden plenamente en la operación entre DataFrame y Serie, los componentes faltantes se alinean automáticamente e introducen valores `NaN`.













<hr>





# Valores nulos en Python

El tratamiento de datos faltantes o nulos (también conocidos en ciencia de datos como *missing*, *NaN* o *NA*) es una de las tareas más comunes e importantes en el análisis de datos, ya que los conjuntos de datos del mundo real rara vez se presentan limpios u homogéneos.

---

## 1. Estrategias Generales para Representar Datos Faltantes

En programación y análisis de datos, existen dos enfoques principales para indicar que un valor está ausente en una tabla o estructura de datos:

*   **Máscaras:** Consiste en la utilización de matrices booleanas completamente independientes o la asignación de bits locales dedicados a indicar el estado nulo de un valor. Este enfoque añade una sobrecarga extra tanto de almacenamiento en memoria como de capacidad de cálculo.
*   **Valores Centinela:** Se trata de elegir convenciones específicas de datos. Puede ser una solución local (como indicar un entero faltante con el número `-9999`) o una convención global (como el uso de `NaN`). Los centinelas reducen el rango de valores válidos representables por el tipo de dato y requieren una lógica de CPU/GPU adicional que a menudo no está optimizada.

### Comparativa entre Sistemas
*   El lenguaje **R** utiliza patrones de bits reservados dentro de cada tipo de datos como valores centinela nativos para indicar la ausencia de datos.
*   El sistema **SciDB** utiliza un byte adicional adjunto a cada celda que indica explícitamente un estado NA.

---

## 2. El Enfoque de Pandas y su Dependencia de NumPy

La forma en que Pandas gestiona la nulidad está directamente limitada por su dependencia del paquete **NumPy**, el cual carece de una noción integrada de valores nulos para tipos de datos que no sean de punto flotante (*float*). 

Para evitar la sobrecarga inmanejable de bifurcar las más de 14 precisiones de enteros de NumPy o utilizar arrays enmascarados complejos, **Pandas optó por utilizar centinelas basados en dos objetos existentes en Python: `None` y `NaN`**.

### `None`: El Faltante Pythónico
Es un objeto especial de tipo `NoneType` (un *singleton* nativo de Python) que indica la ausencia de valor o que una variable está vacía.
*   **Restricciones de almacenamiento:** Solo se puede emplear en arrays de tipo `object` (arrays de objetos de Python).
*   **Rendimiento:** Genera mucha sobrecarga computacional. Las operaciones a nivel de Python son significativamente más lentas que las operaciones optimizadas en tipos nativos de NumPy (como `int` o `float`).
*   **Errores aritméticos:** Realizar agregaciones o agregaciones aritméticas (`+`, `sum()`, `min()`) en un array que contenga un objeto `None` provocará un error de tipo (`TypeError: unsupported operand type(s) for +: 'int' and 'NoneType'`), debido a que la operación entre un entero y un objeto `None` no está definida.

### `NaN`: El Faltante Numérico (*Not a Number*)
Es un valor especial de punto flotante reconocido por todos los sistemas bajo la representación estándar de punto flotante IEEE.
*   **Rendimiento:** Al ser un tipo nativo de punto flotante (`float64`), los arrays que albergan `NaN` soportan operaciones vectorizadas muy rápidas delegadas en código compilado.
*   **Efecto "Virus":** El valor `NaN` actúa como un virus de datos en operaciones aritméticas. Cualquier operación matemática que involucre un `NaN` dará como resultado inexorable otro `NaN` (`1 + np.nan = nan` o `0 * np.nan = nan`).
*   **Agregaciones estadísticas:** Las agregaciones estándar sobre arrays con `NaN` no devuelven error, pero devuelven `nan`, invalidando el cálculo estadístico (`vals.sum(), vals.min(), vals.max() -> (nan, nan, nan)`). 
*   **Funciones Especiales de NumPy:** Para solventarlo, NumPy dispone de funciones específicas que ignoran estos valores faltantes: `np.nansum()`, `np.nanmin()`, `np.nanmax()`, `np.nanprod()` y `np.nanmean()`.
*   **Limitación de Tipo:** `NaN` es específicamente un valor de punto flotante; no hay un valor NaN equivalente nativo para enteros, cadenas u otros tipos en el núcleo de NumPy.

---

## 3. Conversión Automática de Tipos (*Upcasting*)

Pandas opera con `None` y `NaN` de forma casi intercambiable. Cuando un usuario introduce un valor nulo (`None` o `np.nan`) en una estructura cuyo tipo de dato original no admite la nulidad de forma nativa, Pandas realiza un **upcasting** o conversión automática de tipo de manera transparente:

| Clase de Tipo original | Conversión al almacenar un NA | Valor Centinela NA asignado |
| :--- | :--- | :--- |
| **`floating`** (Decimales) | Sin cambios | `np.nan` |
| **`object`** (Objetos/Strings) | Sin cambios | `None` o `np.nan` |
| **`integer`** (Enteros) | Convierte la columna a **`float64`** | `np.nan` |
| **`boolean`** (Booleanos) | Convierte la columna a **`object`** | `None` o `np.nan` |

*Nota:* En Pandas, los datos de texto (cadenas/strings) se guardan siempre de forma predeterminada bajo el dtype `object`. Además de convertir el array de enteros a punto flotante, Pandas convierte automáticamente cualquier objeto `None` introducido en un valor `NaN`.

---

## 4. Funciones Principales para Operar con Nulos en Pandas

Pandas cuenta con herramientas integradas fundamentales para gestionar la falta de datos de manera eficiente:

### A. Detección (`isnull` / `isna` / `notnull`)
*   **`isnull()` / `isna()`**: Evalúan la estructura y devuelven una máscara booleana con valores `True` en aquellas celdas donde el dato está ausente (`NaN` o `None`) y `False` donde hay datos válidos.
*   **`notnull()`**: Realiza exactamente la operación inversa, marcando con `True` los valores válidos y con `False` las ausencias.
*   **Filtrado por máscara:** Las máscaras booleanas resultantes pueden usarse directamente entre corchetes para indexar y filtrar los datos válidos de una estructura (ej. `data[data.notnull()]` o `data[~data.isnull()]`).
*   **Conteo de nulos:** Es una práctica común encadenar la función de detección con una sumatoria para cuantificar las ausencias por cada columna: `df.isna().sum()`.

### B. Eliminación (`dropna`)
Permite filtrar, descartar y limpiar las estructuras eliminando los registros nulos. Dado que en un `DataFrame` bidimensional no se pueden borrar celdas aisladas sin romper la estructura de la tabla, `dropna()` elimina filas o columnas completas bajo los siguientes parámetros de control:

*   **`axis`**: Determina la dirección del filtrado. Por defecto es `0` o `'rows'` (elimina filas completas que tengan nulos). Configurado en `1` o `'columns'` elimina las columnas completas que tengan nulos.
*   **`how`**: Define el criterio de descarte. Su valor por defecto es `'any'` (elimina la fila/columna si tiene al menos un valor nulo). Puede cambiarse a `'all'` para indicar que solo se elimine la fila o columna si *todos* sus elementos son nulos de forma simultánea.
*   **`thresh`**: Configura un umbral numérico estricto. Permite especificar de forma precisa el número mínimo de valores **no nulos** (válidos) requeridos para que la fila o columna se conserve. Por ejemplo, `df.dropna(axis='rows', thresh=len(df.columns)*0.75)` mantendrá solo las filas que tengan al menos un 75% de datos válidos.
*   **`inplace`**: Por defecto, `dropna()` devuelve una copia filtrada y mantiene la estructura original intacta. Si se establece `inplace=True`, la estructura original se modifica directamente en memoria (`data.dropna(inplace=True)`).

### C. Reemplazo e Imputación (`fillna` / `ffill` / `bfill`)
Devuelve una copia de la estructura de datos sustituyendo los nulos por valores válidos bajo diferentes estrategias:

*   **Valor Fijo o Escalar:** Rellena los espacios vacíos con una constante fija, como el número cero (`df.fillna(0)`) o una cadena de texto (`df.fillna("nuevo valor")`).
*   **Imputación Estadística:** Rellena los nulos utilizando métricas calculadas a partir de los datos válidos de la propia columna, como su promedio estadístico: `df[1].fillna(df[1].mean())`.
*   **Métodos de Propagación de Posición:** Rellenan los nulos basándose en la proximidad de otros datos contiguos válidos:
    *   **`ffill()`** (*forward-fill*): Propaga el último valor válido detectado hacia adelante para cubrir los nulos siguientes.
    *   **`bfill()`** (*back-fill*): Propaga el siguiente valor válido detectado hacia atrás para cubrir los nulos precedentes.
    *   *Nota de dirección:* En ambos métodos se puede parametrizar el sentido de la propagación (horizontal o vertical) modificando el argumento `axis` (ej. `df.bfill(axis=1)` realiza un relleno hacia atrás horizontal). Si un valor nulo se encuentra al extremo de la estructura y no cuenta con un valor previo (en `ffill`) o posterior (en `bfill`) para copiarse, el valor `NaN` permanecerá inalterado. En versiones antiguas de Pandas, estas operaciones se realizaban mediante parámetros internos dentro de la función principal: `df.fillna(method='ffill')`.








<hr>








# Agregación y Agrupación de Datos en Pandas

La sumarización eficiente es una parte esencial del análisis de datos. Consiste en reducir grandes volúmenes de registros a un único valor descriptivo descriptivo mediante operaciones estadísticas (como `sum()`, `mean()`, `median()`, `min()`, y `max()`), facilitando la comprensión de la naturaleza de los conjuntos de datos.

---

## 1. Agregación Básica en Pandas

Las agregaciones en Pandas devuelven un único valor cuando se aplican a una `Series`. En el caso de un `DataFrame`, calculan el resultado para **cada columna de forma independiente** de manera predeterminada.

*   **Modificación del eje:** Mediante el argumento `axis='columns'` (o `axis=1`), se puede cambiar la dirección y realizar la agregación de manera horizontal (**por filas**).
*   **Método `describe()`:** Computa de forma automática un conjunto de estadísticas descriptivas estándar para cada columna numérica. Proporciona información clave como el conteo de valores no nulos (`count`), la media (`mean`), la desviación estándar (`std`), los valores mínimos y máximos (`min`, `max`) y los percentiles (25%, 50%, 75%).

### Funciones de Agregación Principales
Todas las funciones están disponibles como métodos tanto en objetos `DataFrame` como `Series`:

| Función | Descripción |
| :--- | :--- |
| `count()` | Número total de elementos (excluye valores nulos). |
| `first()`, `last()` | Primer y último elemento del conjunto. |
| `mean()`, `median()` | Media aritmética y mediana. |
| `min()`, `max()` | Valores mínimo y máximo. |
| `std()`, `var()` | Desviación estándar y varianza de la muestra. |
| `mad()` | Desviación media absoluta. |
| `prod()` | Producto de todos los elementos. |
| `sum()` | Suma de todos los elementos. |

---

## 2. GroupBy: Split, Apply, Combine

Para realizar agregaciones condicionales basadas en dimensiones o etiquetas de índice, se utiliza la operación `.groupby()`. Este concepto se define a través del proceso matemático desarrollado por Hadley Wickham denominado **Split-Apply-Combine**:

1.  **Split (Separar):** Involucra romper, dividir y clasificar el `DataFrame` en subgrupos dependiendo del valor de una o varias claves especificadas.
2.  **Apply (Aplicar):** Consiste en computar una función dentro de cada grupo individual. Esta función puede ser una agregación (reducir el grupo a un número), una transformación o un filtrado de datos.
3.  **Combine (Combinar):** Une los resultados obtenidos en cada subgrupo para consolidarlos en un único objeto o estructura de datos de salida (una matriz, `Series` o `DataFrame`).

### Propiedades y Capacidades del Objeto GroupBy
*   **Evaluación Perezosa (*Lazy Evaluation*):** Al invocar el método `df.groupby('key')`, Pandas no realiza ningún cálculo de manera inmediata. En su lugar, devuelve un objeto especial del tipo `DataFrameGroupBy` (o `SeriesGroupBy`). Este objeto actúa como una vista virtual que almacena las instrucciones de segmentación y espera a que se le aplique una función de agregación para ejecutar la computación de forma optimizada en una sola pasada.
*   **Indexado de Columnas:** Al igual que un `DataFrame`, el objeto `GroupBy` soporta la selección de columnas específicas usando corchetes antes de aplicar la agregación (ej. `df.groupby('key')['columna_objetivo'].mean()`).
*   **Iteración Directa:** Soporta la iteración explícita mediante bucles `for`. En cada iteración, el generador devuelve una tupla compuesta por el nombre del grupo (el valor de la clave) y su sub-DataFrame o sub-Series correspondiente.
*   **Métodos de Envío:** Mediante el uso de metaprogramación en Python, cualquier método válido de un `DataFrame` o `Series` que no esté implementado directamente en el objeto `GroupBy` (como por ejemplo el método `.describe()`) se pasará y ejecutará de forma aislada dentro de cada subgrupo.

---

## 3. Operaciones Avanzadas: Aggregate, Filter, Transform y Apply

Para procesar grupos con un nivel de flexibilidad superior al de las medias o sumas básicas, el objeto `GroupBy` proporciona cuatro métodos fundamentales:

### Agregación Avanzada (`aggregate()` / `agg()`)
Permite calcular múltiples funciones estadísticas de manera simultánea sobre los grupos. Admite varias formas de parametrización:
*   Una cadena de texto con el nombre de la función (ej. `'mean'`).
*   Una lista de funciones o cadenas (ej. `['min', 'median', 'max']`), lo que genera un `DataFrame` con columnas jerárquicas (**MultiIndex**).
*   Un diccionario que asocia columnas específicas con operaciones explícitas (ej. `df.groupby('key').agg({'col1': 'min', 'col2': 'mean'})`).

### Filtrado de Grupos (`filter()`)
Permite descartar o conservar grupos enteros en función de una propiedad booleana evaluada de forma global sobre el grupo completo. Recibe como argumento una función (a menudo una función `lambda`) que procesa cada sub-DataFrame y debe retornar un valor booleano (`True` o `False`). Si el grupo completo no satisface la condición, todos sus registros individuales son eliminados de la estructura final.

### Transformación de Datos (`transform()`)
A diferencia de la agregación, que reduce las dimensiones de los datos, la transformación devuelve una versión modificada de los registros que conserva **la misma forma exacta y dimensiones** que el objeto original. Se utiliza comúnmente para operaciones de normalización, estandarización o centrado de datos, como restar a cada registro la media correspondiente a su grupo:
````
\[\text{Resultado} = x - \mu_{\text{grupo}}\]
````

### Aplicación General (`apply()`)
Es la herramienta más flexible de manipulación por grupos. Permite aplicar una función arbitraria sobre los sub-DataFrames de cada grupo. La función del usuario puede retornar un escalar, una `Series` o un `DataFrame`. El paso de combinación (*Combine*) se adapta de manera automática y une los resultados según el tipo de dato devuelto por la función.

### Opciones para Especificar las Llaves de Separación
Los criterios de división en un `.groupby()` no se limitan a los nombres de las columnas existentes. Se pueden utilizar:
*   Una lista, array, `Series` o índice externo cuya longitud coincida exactamente con la del `DataFrame` que se está agrupando.
*   Un diccionario o una `Series` que mapee los valores actuales del índice a nuevos nombres de grupos.
*   Cualquier función nativa o personalizada de Python (como `str.lower` para normalizar y agrupar cadenas de texto presentes en las etiquetas del índice).
*   Una lista combinada de cualquiera de las opciones anteriores, lo que segmenta los datos en múltiples niveles y genera un **MultiIndex** (índices jerárquicos).

---

## 4. Pivot Tables (Tablas Dinámicas)

Las tablas dinámicas son conceptualmente versiones **multidimensionales** de la agregación `GroupBy`. Mientras que `GroupBy` segmenta y combina datos a lo largo de un eje unidimensional (normalmente las filas), la tabla dinámica (`pivot_table`) distribuye las operaciones estadísticas en una cuadrícula o matriz bidimensional.

### Sintaxis General y Argumentos Principales
````
df.pivot_table(data, values=None, index=None, columns=None,
               aggfunc='mean', fill_value=None, margins=False,
               dropna=True, margins_name='All')
````

*   `index`: Especifica la variable o variables cuyas categorías se colocarán en las **filas** de la cuadrícula.
*   `columns`: Especifica la variable o variables cuyas categorías se colocarán en las **columnas** de la cuadrícula.
*   `values`: Determina la columna numérica sobre la cual se aplicará la función de agregación. Si se define un diccionario en `aggfunc`, este parámetro se puede omitir.
*   `aggfunc`: Controla la función de agregación que se aplicará a los datos. Por defecto calcula la media (`'mean'`). Al igual que en `GroupBy`, puede recibir una lista de funciones o un diccionario para aplicar operaciones distintas a columnas diferentes.
*   `fill_value` y `dropna`: Permiten gestionar el tratamiento de los valores nulos o faltantes resultantes en la cuadrícula.
*   `margins=True`: Añade de forma automática filas y columnas adicionales que muestran los totales globales y subtotales de la cuadrícula. El nombre de estas etiquetas se puede personalizar con el argumento `margins_name` (cuyo valor predeterminado es `"All"`).
*   **Análisis Multi-nivel:** Al igual que en `GroupBy`, se pueden pasar listas de variables tanto al argumento `index` como a `columns`. Esto, combinado con funciones de discretización de rangos como `pd.cut()` (agrupación por intervalos definidos) o `pd.qcut()` (agrupación por cuantiles), permite construir resúmenes estadísticos complejos de más de dos dimensiones.






<hr>



# Combinar Datasets en Pandas: Concat, Append, Merge y Join

Este repositorio contiene una guía práctica sobre cómo realizar operaciones avanzadas de manipulación y combinación de datos utilizando **Pandas** y **NumPy**. Incluye desde la concatenación simple hasta cruces complejos utilizando un caso de estudio real con datos demográficos de los Estados Unidos.

---

## 📌 Tabla de Contenidos
1. [Concatenación Sencilla (pd.concat)](#1-concatenación-sencilla-pdconcat)
2. [Manejo de Índices Duplicados](#2-manejo-de-índices-duplicados)
3. [Combinación con Joins aritméticos](#3-combinación-con-joins-aritméticos)
4. [Fusión Avanzada de Datos (pd.merge)](#4-fusión-avanzada-de-datos-pdmerge)
5. [Caso Práctico: Densidad de Población en EE. UU.](#5-caso-práctico-densidad-de-población-en-ee-uu)

---

## 1. Concatenación Sencilla (`pd.concat`)

La función `pd.concat()` permite unir colecciones de objetos tipo `Series` o `DataFrame` de forma similar a `np.concatenate` en NumPy, pero con opciones más potentes.

* **Por filas (Eje 0):** Operación por defecto (`axis=0`).
* **Por columnas (Eje 1):** Alineación horizontal usando `axis=1`.

```python
# Ejemplo de concatenación por columnas
pd.concat([df3, df4], axis=1)
```

## 2. Manejo de Índices Duplicados

A diferencia de NumPy, Pandas **mantiene los índices originales** al concatenar, lo que puede generar duplicaciones en el dataset resultante. Existen tres formas de gestionar este comportamiento:

* **Permitir duplicados:** Comportamiento por defecto.
* **Capturar duplicados como error:** Utilizando `verify_integrity=True` para lanzar una excepción si hay solapes.
* **Ignorar el índice:** Utilizando `ignore_index=True` para generar un nuevo índice entero incremental.
* **Índices jerárquicos (MultiIndex):** Utilizando el parámetro `keys=[...]` para etiquetar la procedencia de cada fuente de datos.

## 3. Combinación con Joins aritméticos

Cuando los `DataFrames` no comparten exactamente las mismas columnas, se puede especificar la intersección de conjuntos:

* **Outer Join (`join='outer'`):** Unión completa de las columnas (rellena los vacíos con `NaN`). Es el comportamiento por defecto.
* **Inner Join (`join='inner'`):** Intersección estricta. Solo mantiene las columnas que existen en todos los datasets.

## 4. Fusión Avanzada de Datos (`pd.merge`)

La función `pd.merge()` implementa operaciones de álgebra relacional de alto rendimiento en memoria, categorizadas en tres tipos de relaciones:

### Categorías de Cruces
* **One-to-one (Uno a uno):** Unión simple basada en claves compartidas con valores únicos.
* **Many-to-one (Muchos a uno):** Una de las claves contiene elementos duplicados; el DataFrame resultante preserva dicha estructura.
* **Many-to-many (Muchos a muchos):** Ambas columnas clave tienen duplicados, generando una combinación cruzada de los elementos que coinciden.

### Especificación de Claves
* **`on`:** Define la columna clave común si tiene el mismo nombre en ambas tablas.
* **`left_on` y `right_on`:** Permite mapear claves que tienen nombres diferentes en cada tabla.
* **`left_index` y `right_index`:** Permite realizar el cruce utilizando los índices en lugar de columnas (también simplificado con el método `.join()`).

### Sufijos para Conflictos
Si existen columnas con el mismo nombre que no forman parte del cruce, Pandas añade automáticamente sufijos `_x` e `_y`. Estos pueden personalizarse con el parámetro `suffixes=['_Sufijo1', '_Sufijo2']`.

---

## 5. Caso Práctico: Densidad de Población en EE. UU.

Se lleva a cabo un ejercicio de limpieza y combinación (*Data Wrangling*) utilizando tres fuentes de datos en formato CSV:
1. **`state-population.csv`**: Histórico de población por estado (`total` y `under18`).
2. **`state-areas.csv`**: Área física en millas cuadradas de cada estado/territorio.
3. **`state-abbrevs.csv`**: Abreviaturas oficiales de los estados.

### Flujo de Trabajo Técnico:
1. **Unión Inicial (Many-to-one):** Combinación de población y abreviaturas mediante `how='outer'` para identificar pérdidas de registros.
2. **Data Cleaning:** Detección de nulos en territorios no tabulados (como Puerto Rico `PR` y el total de `USA`). Corrección manual de datos faltantes y eliminación de filas irrelevantes mediante `.dropna()`.
3. **Segunda Unión:** Cruce con la tabla de áreas basándose en el nombre completo del estado.
4. **Análisis de Datos:** Filtrado del censo del año **2010** para la población `total` mediante la función `.query()`.
5. **Cálculo Final:** Creación de la métrica `density` (`population / area (sq. mi)`) y ordenación de los resultados.





<hr>




# Obtención de Datos Mediante APIs en Python

Este repositorio contiene una guía detallada y ejemplos prácticos sobre cómo consumir interfaces de programación de aplicaciones (**APIs**) utilizando Python, centrándose principalmente en el protocolo HTTP y la biblioteca `requests`.

---

## 1. Introducción a las APIs

Una **API (Application Programming Interface)** es un conjunto de reglas y protocolos que permiten a diferentes aplicaciones interactuar y comunicarse entre sí. Actúan como un puente técnico que permite a un software solicitar datos o realizar acciones en un servidor remoto de manera estructurada, automatizada y estandarizada, sin necesidad de conocer los detalles internos de la implementación del servidor.

---

## 2. El Protocolo HTTP y la Arquitectura Cliente-Servidor

El **Protocolo de Transferencia de Hipertexto (HTTP)** es la norma subyacente que rige la World Wide Web para la transmisión y solicitud de documentos e información. La comunicación se basa en un ciclo continuo de **Petición (Request)** y **Respuesta (Response)**:

1. **Cliente (Frontend):** Envía una petición HTTP formal al servidor web.
2. **Servidor (Backend / Base de datos):** Procesa la solicitud, interactúa con sus propios servicios o bases de datos si es necesario, y devuelve una respuesta estructurada al cliente.

### Métodos HTTP más comunes
Para indicarle al servidor qué acción queremos realizar sobre un recurso, se utilizan diferentes verbos o métodos de solicitud:

*   **GET:** Se utiliza exclusivamente para recuperar o leer datos de un servidor. No modifica el estado del recurso.
*   **POST:** Se usa para enviar nuevos datos al servidor con el fin de crear un nuevo recurso.
*   **PUT:** Se emplea para actualizar o reemplazar por completo un recurso existente en el servidor.
*   **DELETE:** Se utiliza para eliminar un recurso específico del servidor.

### Parámetros y Códigos de Estado (Status Codes)
Las peticiones HTTP pueden incluir **parámetros** (en la URL o en el cuerpo) para filtrar o especificar los datos requeridos. Como respuesta, el servidor devuelve un código numérico estándar que indica el resultado de la operación:

*   **2xx (Éxito):** Por ejemplo, `200 OK` significa que la petición fue procesada correctamente.
*   **4xx (Errores del Cliente):** Por ejemplo, `404 Not Found` (el recurso no existe) o `429 Too Many Requests` (límite de peticiones excedido).
*   **5xx (Errores del Servidor):** El servidor falló al intentar procesar una solicitud que aparentemente era válida.

---

## 3. La Biblioteca `requests` en Python

La biblioteca `requests` es el estándar de facto en Python para realizar solicitudes HTTP debido a su sintaxis intuitiva y humana en comparación con los módulos nativos del lenguaje.

### Instalación
Para incorporar la biblioteca al entorno de desarrollo se ejecuta:
```bash
pip install requests
```

### Importación básica de librerías esenciales
```python
import requests
import zipfile
import pandas as pd
```

---

## 4. Ejemplos Prácticos de Peticiones y Manejo de Respuestas

### 4.1. Descarga y Almacenamiento de Archivos Binarios (Imágenes)
Es posible realizar una petición `GET` para descargar elementos binarios de la web utilizando la propiedad `.content` de la respuesta, la cual obtiene los datos directamente en bytes:

```python
# Definición de la URL del recurso
url = "https://googleusercontent.com"

# Realizar la petición GET
image = requests.get(url)

# Comprobar el código de estado (debería retornar <Response [200]>)
print(image)

# Imprimir el contenido en bytes crudos (b'\xff\xd8...')
print(image.content)

# Guardar los bytes en un archivo local en modo de escritura binaria ('wb')
with open("data/dotcsv.jpg", 'wb') as f:
    f.write(image.content)
```

### 4.2. Lectura Directa de un CSV en la Web usando `pandas`
La biblioteca `pandas` permite consumir URLs directamente para estructurar un conjunto de datos en un objeto `DataFrame` de manera inmediata sin necesidad de usar `requests` explícitamente:

```python
# Cargar un archivo CSV directamente desde una URL pública
df_inflation = pd.read_csv('https://datahub.io')

# Visualizar las primeras 5 filas del DataFrame
print(df_inflation.head())

# Filtrar el DataFrame según condiciones específicas
df_spain = df_inflation[df_inflation['Country'] == \"Spain\"]
print(df_spain)
```

### 4.3. Consumo de una API Pública con Respuestas JSON
La mayoría de las APIs modernas devuelven la información en formato **JSON (JavaScript Object Notation)**. La biblioteca `requests` cuenta con el método incorporado `.json()` para transformar esta respuesta en un diccionario nativo de Python:

```python
# Función reutilizable para obtener y decodificar datos JSON
def get_joke(url):
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()  # Convierte el formato JSON a diccionario de Python
        return data
    else:
        print("Error en la solicitud: ", response.status_code)

# Endpoint base de la API de Chuck Norris
url_random = "https://chucknorris.io"
print(get_joke(url_random))

# Ejemplo de uso de parámetros directamente integrados en el Endpoint (Filtro por categoría)
url_food = "https://chucknorris.io?category=food"
print(get_joke(url_food))
```

### 4.4. Envío de Parámetros Dinámicos (API de Clima)
En lugar de concatenar texto manualmente en la URL, se recomienda utilizar el parámetro `params` del método `requests.get()`, el cual acepta un diccionario y construye automáticamente la query string (por ejemplo: `?latitude=40.4165&longitude=-3.7026...`):

```python
url_weather = "https://open-meteo.com"

# Estructura de parámetros requeridos por el servidor
parametros = {
    "latitude": 40.4165,
    "longitude": -3.7026,
    "current_weather": "true"
}

respuesta = requests.get(url_weather, params=parametros)

if respuesta.status_code == 200:
    datos = respuesta.json()
    clima = datos["current_weather"]
    
    print(f"Temperatura actual: {clima['temperature']} °C")
    print(f"Velocidad del viento: {clima['windspeed']} km/h")
else:
    print("Error de conexión:", respuesta.status_code)
```

### 4.5. Procesamiento y Estructuración de datos complejos en DataFrames
Cuando una API devuelve colecciones de datos complejas dentro de un objeto JSON, podemos aislar la lista de interés y transformarla inmediatamente en una tabla manipulable:

```python
space_url = "http://thespacedevs.com"
response_sp = requests.get(space_url)

if response_sp.status_code == 200:
    # Convertir los resultados de la API directamente en un DataFrame de Pandas
    df_astronauts = pd.DataFrame(response_sp.json()['results'])
    print(df_astronauts.head())
else:
    print(f"Estado de la respuesta: {response_sp.status_code}")
```





<hr>





# Python: Lectura, Escritura y Gestión de Archivos

Este repositorio contiene los mecanismos fundamentales para interactuar con el almacenamiento local mediante Python. Aprenderás a abrir y modificar ficheros planos, procesar datos tabulares (CSV, Excel), intercambiar estructuras de objetos complejos (JSON, Pickle), descomprimir archivos comprimidos (ZIP) y automatizar el sistema de archivos del sistema operativo a través del módulo `os`.

---

## Índice
1. [Fundamentos de Archivos y Rutas](#1-fundamentos-de-archivos-y-rutas)
2. [Gestión Nativa de Ficheros (`open`)](#2-gestión-nativa-de-ficheros-open)
3. [Formatos Tabulares I: Archivos CSV](#3-formatos-tabulares-i-archivos-csv)
4. [Formatos Tabulares II: Archivos Excel](#4-formatos-tabulares-ii-archivos-excel)
5. [Notación de Objetos JSON](#5-notación-de-objetos-json)
6. [Ficheros de Texto Plano (`.txt` y `.tsv`)](#6-ficheros-de-texto-plano-txt-y-tsv)
7. [Archivos Comprimidos (`.zip`)](#7-archivos-comprimidos-zip)
8. [Serialización de Objetos (`pickle`)](#8-serialización-de-objetos-pickle)
9. [Codificación de Caracteres (`Encoding`)](#9-codificación-de-caracteres-encoding)
10. [Automatización del Sistema Operativo (`os` y `shutil`)](#10-archivos-y-carpetas-módulo-os)

---

## 1. Fundamentos de Archivos y Rutas

Un **archivo es un conjunto de datos almacenados en el ordenador en forma de bits**. Toda la información se organiza bajo un formato específico que el ordenador traduce a binario para su procesamiento. 

### Anatomía Estructural de un Archivo
*   **Header (Cabecera):** Almacena los metadatos esenciales del archivo, como su nombre, tamaño o tipo de formato.
*   **Data (Contenido):** El cuerpo de datos o contenido propiamente dicho del archivo.
*   **End of file (EOF):** Un carácter especial integrado que indica de forma inequívoca el final del archivo.

### Rutas de Acceso (File Paths)
Para acceder a un archivo se requiere conocer tres elementos: el **Folder path** (directorio de ubicación), el **File name** (nombre) y su **Extension** (sufijo tras el punto).
*   **Rutas Relativas:** Toman como referencia el directorio actual en el que está apuntando el programa de Python. El uso de `..` retrocede un nivel hacia atrás en el árbol de carpetas (ej: `../dog_breeds.txt`).
*   **Rutas Absolutas:** Describen la ruta completa desde la raíz del sistema de discos (ej: `C:/Users/usuario/...`). **No se recomienda su uso** en desarrollo de software porque rompe la portabilidad del código al ejecutarlo en otros ordenadores.

---

## 2. Gestión Nativa de Ficheros (`open`)

Python cuenta con funciones *built-in* nativas que permiten manipular archivos directamente sin importar librerías externas mediante la función **`open()`**.

### Sintaxis y Contexto Seguro (`with open`)
Modificar o leer archivos manteniéndolos abiertos de forma persistente genera bloqueos en memoria y errores. La buena práctica dicta usar la sentencia de control de contexto **`with open()`**. El archivo se abre, se vuelcan las operaciones deseadas en su bloque indentado y, al salir de él, Python **cierra automáticamente el archivo** de forma segura.

```python
with open("filename.txt", "mode") as file_object:
    # Bloque de operaciones internas
    pass
```

### Modos Fundamentales de Apertura
*   **`'r'` (Read):** Modo por defecto. Abre el archivo estrictamente para lectura. Lanza un error si el fichero no existe.
*   **`'w'` (Write):** Modo de escritura. Si el archivo ya existe, **borra por completo todo su contenido anterior** antes de escribir. Si no existe, crea un archivo nuevo.
*   **`'a'` (Append):** Modo de anexado. Añade el contenido nuevo **al final** del archivo existente, respetando los datos previos sin machacarlos.

### Métodos de Lectura Integrados
*   `.read()`: Vuelca el archivo entero de golpe devolviendo un único String gigante.
*   `.readlines()`: Lee todo el archivo y **devuelve una Lista de Python**, donde cada elemento es una línea del texto en formato String (conservando saltos de línea `\n`).
*   **Iteración por Línea (Recomendado):** Se puede recorrer el objeto lector directamente en un bucle `for` para procesar el fichero de forma secuencial línea a línea sin saturar la memoria RAM.

---

## 3. Formatos Tabulares I: Archivos CSV

El formato **CSV (*Comma Separated Values*) es el estándar de la industria para el almacenamiento e intercambio de datos tabulares bidimensionales**. Es un archivo de texto plano de alta eficiencia que ocupa muy poco espacio en disco debido a su sencillez.

### Particularidades Técnicas
*   **Delimitadores:** Aunque su nombre indica separación por comas, **se recomienda trabajar con CSVs cuyo separador sea el punto y coma (`;`)**. Esto evita que el intérprete confunda la coma utilizada como separador decimal en los números flotantes con el separador de columnas del dataset.
*   **Estructura:** La primera línea suele actuar como cabecera (*header*) declarando el nombre de las columnas. Las filas se delimitan mediante saltos de línea convencionales.

### Procesamiento con Pandas
La librería `pandas` provee las funciones óptimas de lectura y escritura:
*   **Lectura (`pd.read_csv()`):** Transforma el texto plano en un objeto estructurado `DataFrame`. Parámetros clave: `sep` (indica el carácter delimitador, ej: `';'`), `index_col` (establece una columna como índice del DataFrame), `usecols` (permite cargar únicamente un subconjunto de columnas específicas) y `dtype` (fuerza la tipificación manual de columnas durante la carga).
*   **Escritura (`df.to_csv()`):** Guarda las modificaciones en un archivo `.csv` local. Se aconseja añadir el argumento `index=False` para evitar que el índice numérico implícito se guarde de forma permanente como una columna adicional.

---

## 4. Formatos Tabulares II: Archivos Excel

A diferencia del CSV, las extensiones de Microsoft Excel (`.xlsx`, `.xls`) codifican la información de manera comprimida e integrada. Es un formato mucho más flexible que permite albergar múltiples hojas de datos, celdas de texto libre ajenas a la tabla principal y configuraciones complejas.

### Lectura con Pandas (`pd.read_excel()`)
Para interactuar con libros de Excel en Python es común utilizar motores de lectura como la librería `openpyxl`. Al leer con Pandas, se configuran argumentos especializados para aislar la tabla requerida:
*   `sheet_name`: Especifica la hoja exacta del libro a leer (por nombre en string o por su índice numérico base cero).
*   `header`: Define el número de fila exacto en el que comienzan las cabeceras de columnas del dataset.
*   `usecols`: Permite filtrar el rango de columnas nativas de Excel que se desean importar (ej: `'B:K'`).
*   `skiprows`: Ignora un número de filas iniciales o un listado explícito de filas específicas durante el volcado de datos.

Para escribir DataFrames de vuelta a Excel, se invoca directamente al método `.to_excel()` especificando la ruta destino.

---

## 5. Notación de Objetos JSON

**JSON (*JavaScript Object Notation*) es un formato de texto plano estructurado de clave/valor independiente del lenguaje**, usado masivamente para el intercambio de información entre clientes y servidores web.

### Flexibilidad vs Tabulación
JSON abandona la rigidez dimensional de las filas y columnas para ganar flexibilidad. En una sola variable se pueden anidar listas, textos u otros objetos complejos empaquetados bajo llaves `{}`. En Python, **un archivo JSON se traduce de forma nativa a un Diccionario (`dict`)**.

### Interacción con la Librería Estándar `json`
*   `json.dump(obj, file)`: Serializa un objeto o diccionario de Python y lo guarda físicamente dentro de un archivo `.json` externo. *(Tip técnico: Para guardar estados de un objeto propio de una clase, se extrae previamente su mapa asociativo llamando al atributo interno `objeto.__dict__`)*.
*   `json.load(file)`: Lee un archivo `.json` local y reconstruye de manera automática la estructura de datos mapeándola a un diccionario ejecutable dentro del programa.

Pandas también permite aplanar estructuras JSON simétricas y cargarlas como tablas relacionales convencionales ejecutando la función `pd.read_json(..., lines=True)` si el fichero sigue el formato JSON Lines.

---

## 6. Ficheros de Texto Plano (`.txt` y `.tsv`)

Los archivos `.txt` carecen de un formato formal preestablecido y se limitan a almacenar cadenas de texto libre. Sin embargo, cuando se emplean para coleccionar datos en bruto, suelen incorporar esquemas de separación estructurados:
*   **Separación por Tabulaciones:** Los archivos estructurados con tabuladores (comúnmente guardados bajo la extensión específica **`.tsv`** o `.txt`) se procesan directamente con la función `pd.read_csv()` configurando el parámetro de escape de tabulación **`sep='\t'`**.

---

## 7. Archivos Comprimidos (`.zip`)

Cuando se trabaja con repositorios masivos, los datos suelen distribuirse empaquetados para optimizar la transferencia de red. Python integra el módulo nativo **`zipfile`** para manipular contenedores comprimidos sin necesidad de software de terceros.

```python
import zipfile

# Descompresión masiva de un contenedor ZIP
with zipfile.ZipFile('data/laligaZIP.zip', 'r') as zip_ref:
    zip_ref.extractall('data') # Descomprime todo el contenido en la carpeta destino
```

---

## 8. Serialización de Objetos (`pickle`)

El módulo **`pickle` es la herramienta nativa de Python que permite serializar y deserializar objetos**. La serialización es el proceso mediante el cual un objeto en memoria (un diccionario, una lista, un DataFrame o una instancia de una clase personalizada) se transforma en un **stream o flujo de bytes** para poder almacenarse físicamente en un archivo o transmitirse a través de una red.

### Utilidad Práctica
A diferencia de formatos de texto plano como JSON (que solo admiten tipos de datos básicos y estructuras jerárquicas simples), `pickle` puede congelar en el disco duro **cualquier estructura u objeto de Python** conservando su tipo, sus propiedades y su estado exacto para recuperarlo idénticamente más adelante. Es ampliamente utilizado en Data Science para guardar modelos de Machine Learning ya entrenados.

### Modos Binarios Obligatorios
Dado que `pickle` no genera texto legible por humanos sino flujos de bytes puros, la apertura de los archivos mediante la función `open()` requiere obligatoriamente el uso del flag **`b` (binary)** junto a los modos habituales:
*   **`'wb'` (Write Binary):** Para serializar y escribir el objeto en el disco mediante la función `pickle.dump()`.
*   **`'rb'` (Read Binary):** Para leer los bytes del archivo y reconstruir el objeto original en memoria mediante `pickle.load()`.

```python
import pickle

# Ejemplo de escritura (Serialización)
with open('data/importante', 'wb') as f:
    pickle.dump(objeto_python, f)

# Ejemplo de lectura (Deserialización)
with open('data/importante', 'rb') as f:
    objeto_recuperado = pickle.load(f)
```

---

## 9. Codificación de Caracteres (`Encoding`)

Todos los caracteres y cadenas de texto (*strings*) se almacenan internamente en el ordenador como conjuntos de bytes. El proceso de traducir caracteres a bytes se conoce como ***encoding***, mientras que la operación inversa (pasar de bytes a texto legible) se llama ***decoding***.

### El Conflicto de la Representación de Datos
Los strings se suelen mapear en un espacio de bits que va de 0 a 255. Debido a que en esa combinación limitada de bits no caben todos los caracteres e idiomas del planeta, **el significado de una combinación de bits específica varía según el *encoding* que se utilice**. 

Por ejemplo, caracteres comunes como la "A" mayúscula se representan igual en casi todas las tablas, pero los bits reservados para caracteres especiales como la **"Ñ"** o las tildes se interpretan de formas completamente distintas según la región, provocando errores de lectura o la aparición de símbolos corruptos (como visualizar *"EspaÃ­as"* o *"EspaÃąa"*).

### Codificaciones Clave en Python
1.  **`'utf-8'`:** Es el estándar moderno más extendido en la industria. Engloba la inmensa mayoría de los caracteres de casi todos los lenguajes del planeta. Es el formato recomendado para trabajar sin conflictos.
2.  **`'unicode'`:** Estándar universal diseñado para la compatibilidad total de textos.
3.  **`'ascii'`:** Codificación americana básica. Solo utiliza 7 bits y contiene 128 caracteres. Lanza un error inmediato de tipo `UnicodeDecodeError` si el archivo contiene tildes, eñes o caracteres especiales ajenos al inglés.
4.  **`'latin'` (o `iso8859`):** Diseñado para cubrir las necesidades de los idiomas de Europa occidental, Oceanía y Latinoamérica.

```python
# Especificación explícita del encoding al leer un archivo en Pandas
import pandas as pd
df = pd.read_csv('data/encoding.csv', encoding='utf-8')
```

---

## 10. Archivos y Carpetas (Módulo `os`)

La automatización de la lectura, escritura, renombrado, borrado y movimiento de archivos entre directorios permite agilizar flujos de trabajo repetitivos y tediosos. Para interactuar directamente con el sistema de archivos del sistema operativo, Python proporciona el módulo integrado **`os`**.

### Funciones de Navegación y Rutas
*   **`os.getcwd()`:** *Get Current Working Directory*. Devuelve un string con la ruta absoluta del directorio de trabajo en el que está apuntando el intérprete de Python en ese momento. Es la base para estructurar correctamente las rutas relativas.
*   **`os.chdir('ruta')`:** *Change Directory*. Cambia dinámicamente el directorio de trabajo actual del programa hacia la ubicación indicada.
*   **`os.path.join('directorio', 'archivo')`:** Concatena carpetas y nombres de archivos de forma inteligente, insertando automáticamente las barras separadoras correctas (`/` o `\`) compatibles con el sistema operativo anfitrión (Windows, Linux o macOS).

### Inspección y Búsqueda de Ficheros
*   **`os.listdir()`:** Devuelve una lista con todos los nombres de los archivos y subcarpetas contenidos en el directorio de trabajo actual. Es ideal para recorrer colecciones en bucles `for` y filtrar elementos por su extensión mediante métodos como `.endswith('.txt')`.
*   **`os.walk('ruta')`:** Generador de alta potencia que bucea recursivamente por un directorio y todas sus subcarpetas. En cada iteración devuelve una tupla con tres elementos: la ruta de la carpeta actual, una lista de sus subcarpetas y una lista de sus archivos.

### Operaciones Operativas Críticas
*   **`os.mkdir('nombre')`:** Crea una nueva carpeta o directorio en la ruta indicada.
*   **`os.rmdir('nombre')`:** Elimina una carpeta existente (siempre que se encuentre vacía).
*   **`os.remove('ruta_fichero')`:** Borra de forma definitiva un archivo del almacenamiento físico.
*   **`shutil.move('origen', 'destino')`:** Función importada de la librería complementaria `shutil` que permite mover o trasladar físicamente un archivo de una carpeta a otra.

```python
import os
import shutil

# Comprobar el directorio y listar archivos .txt
print("Directorio actual:", os.getcwd())
for archivo in os.listdir():
    if archivo.endswith('.txt'):
        print("Fichero de texto encontrado:", archivo)

# Construcción de rutas y movimiento seguro
ruta_origen = os.path.join(os.getcwd(), "fichero.txt")
shutil.move(ruta_origen, "data")
```




<hr>








# Visualización de Datos con Matplotlib

**Matplotlib es una librería de visualización de datos multiplataforma construida sobre arrays de NumPy y diseñada para trabajar con el ecosistema amplio de SciPy**. Fue creada por John Hunter en 2002, originalmente como un parche para IPython que permitiera el trazado interactivo al estilo de MATLAB a través de [gnuplot](http://gnuplot.info) desde la línea de comandos. 

El proyecto recibió un gran impulso inicial al ser adoptado por el *Space Telescope Science Institute* (los desarrolladores detrás del telescopio Hubble), institución que apoyó financieramente el desarrollo de Matplotlib y amplió enormemente sus capacidades.

Una de las características más importantes de Matplotlib es su **capacidad de funcionar bien con muchos sistemas operativos y backends de gráficos**, soportando docenas de ellos y múltiples tipos de salida. Este enfoque multiplataforma ha conducido a una gran base de usuarios, a una activa comunidad de desarrolladores y a su ubicuidad dentro del mundo científico de Python.

En los últimos años, nuevas herramientas basadas en la web (D3js, HTML5 canvas) o en el lenguaje R (ggplot, ggvis) han hecho que la interfaz clásica de Matplotlib se sienta anticuada. Sin embargo, sigue siendo una pieza vital de la pila de visualización debido a su robustez como motor gráfico. Actualmente, sirve de base y envoltura (*wrapper*) para APIs más limpias y modernas, como **Seaborn**, [ggpy](http://github.io), [HoloViews](http://holoviews.org), [Altair](http://github.io) e **incluso el propio Pandas**. A pesar de estos envoltorios, a menudo sigue siendo útil sumergirse en la sintaxis de Matplotlib para ajustar la salida final del gráfico.

---

## 🛠️ Configuración General y Estilos

### Importar Matplotlib
Al igual que se utiliza `np` para NumPy y `pd` para Pandas, existe una abreviatura estándar por convención para las importaciones de Matplotlib:
```python
# import matplotlib as mpl
import matplotlib.pyplot as plt
```
La interfaz `plt` es la que se utiliza más a menudo a lo largo de la creación de visualizaciones.

### Ajustes del Estilo
Se utiliza la directiva `plt.style` para elegir los estilos estéticos adecuados para las figuras.
* **Estilo clásico:** Asegura que los gráficos utilicen el estilo clásico de Matplotlib mediante el comando:
  ```python
  plt.style.use('classic')
  ```
* **Estilos disponibles:** Se puede consultar la lista de hojas de estilo por defecto compatibles con el sistema (disponibles a partir de la versión 1.5 de Matplotlib) ejecutando:
  ```python
  print(plt.style.available)
  ```

---

## 🖥️ ¿`show()` o no `show()`?: Cómo Mostrar Gráficos

La forma de ver y interactuar con los gráficos de Matplotlib depende completamente del contexto. Los tres contextos aplicables son: el uso de Matplotlib en un script, en una terminal de IPython, o en un notebook de IPython.

### 1. Plotting desde un Script (.py)
Si se utiliza Matplotlib desde un script independiente, la función `plt.show()` es la herramienta adecuada.
* **Función:** Inicia un bucle de eventos, busca todos los objetos figurativos actualmente activos y abre una o más ventanas interactivas que muestran la figura o figuras.
* **Regla de oro:** El comando `plt.show()` debe usarse **sólo una vez por sesión de Python** y se ve más a menudo al final del script. Múltiples comandos `show()` pueden llevar a un comportamiento impredecible dependiente del backend y deben evitarse.

Un ejemplo de script (*myplot.py*) sería:
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)

plt.plot(x, np.sin(x))
plt.plot(x, np.cos(x))

plt.show()
```

### 2. Plotting desde una Consola Interactiva de IPython
Puede ser muy conveniente utilizar Matplotlib de forma interactiva dentro de un shell de IPython, ya que este sistema está construido para trabajar bien con Matplotlib si se especifica su modo.
* **Activación:** Se habilita este modo usando el comando mágico `%matplotlib` después de iniciar `ipython`:
  ```ipython
  In: %matplotlib
  Using matplotlib backend: TkAgg
  
  In: import matplotlib.pyplot as plt
  ```
* **Visualización:** En este punto, cualquier comando de trazado `plt` hará que se abra una ventana de figura, y se pueden ejecutar otros comandos para actualizar el trazado. No es necesario utilizar `plt.show()`.
* **Actualización:** Algunos cambios (como la modificación de las propiedades de las líneas que ya están dibujadas) no se dibujarán automáticamente; para forzar una actualización se utiliza `plt.draw()`.

### 3. Plotting desde un Notebook IPython (Jupyter Notebook)
El notebook IPython es una herramienta de análisis de datos interactiva basada en el navegador que puede combinar narrativa, código, gráficos, elementos HTML y más en un único documento ejecutable. El plotting interactivo funciona de forma similar al shell de IPython, pero ofrece opciones para incrustar los gráficos directamente en el cuaderno:
* `%matplotlib notebook`: Conduce a gráficos **interactivos** incrustados dentro del notebook.
* `%matplotlib inline`: Conduce a imágenes **estáticas (PNG)** de tu gráfico incrustadas en el notebook (opción generalmente más usada).

---

## 💾 Guardar Figuras en Archivos

Matplotlib tiene la capacidad de guardar figuras en una amplia variedad de formatos de forma nativa a través del comando `savefig()`.

```python
# Ejemplo de guardado de una figura almacenada en la variable 'fig'
fig.savefig('my_figure.png')
```

### Características del Guardado:
* **Inferencia de formato:** El formato de archivo se infiere automáticamente a partir de la extensión del nombre de archivo dado (`.png`, `.jpg`, `.pdf`, `.svg`, etc.).
* **Formatos soportados:** Dependen de los backends instalados. Se puede comprobar la lista de tipos de archivos soportados en el sistema actual utilizando el método del objeto *canvas* de la figura:
  ```python
  fig.canvas.get_supported_filetypes()
  ```
* **Independencia:** Al guardar la figura directamente en un archivo, no es necesario utilizar `plt.show()` o los comandos de visualización interactiva relacionados.

---

## 🔄 Dos Interfaces por el Precio de Una

Una característica potencialmente confusa de Matplotlib es su doble interfaz: una cómoda interfaz basada en estados al estilo de MATLAB, y una interfaz más potente orientada a objetos.

### 1. Interfaz Estilo MATLAB
Gran parte de la sintaxis refleja el hecho de que Matplotlib se escribió originalmente como una alternativa en Python para los usuarios de MATLAB. Las herramientas de estilo MATLAB están contenidas en la interfaz pyplot (`plt`). 

Esta interfaz es ***stateful*** (mantiene un seguimiento de la figura y los ejes "actuales", que es donde se aplican todos los comandos `plt`). Se puede obtener una referencia a estos componentes usando las rutinas `plt.gcf()` (*get current figure*) y `plt.gca()` (*get current axes*). Aunque es rápida y conveniente para gráficos simples, se vuelve torpe si se desea interactuar con varios paneles a la vez o volver a editar un panel previo.

**Ejemplo de sintaxis:**
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)

plt.figure() # Crear una figura de gráfico

# Crear el primero de los dos paneles y fijar el eje actual
plt.subplot(2, 1, 1) # (filas, columnas, número de panel)
plt.plot(x, np.sin(x))

# Crear el segundo panel y fijar el eje actual
plt.subplot(2, 1, 2)
plt.plot(x, np.cos(x))
```

### 2. Interfaz Orientada a Objetos
Está pensada para situaciones más complicadas y para cuando se quiere tener un control absoluto sobre la figura. En lugar de depender de una noción de figura o ejes "activos", las funciones de trazado son *métodos* de objetos explícitos `Figure` y `Axes`. 

**Ejemplo de sintaxis:**
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)

# Crear una rejilla de gráficos de forma explícita
# 'fig' será un objeto Figure y 'ax' será un array de objetos Axes
fig, ax = plt.subplots(2)

# Llamar al método plot() en el objeto apropiado
ax[0].plot(x, np.sin(x))
ax[1].plot(x, np.cos(x))
```

La diferencia fundamental radica en que, en gráficos sencillos, la elección es una cuestión de preferencia, pero el enfoque orientado a objetos se vuelve una necesidad a medida que los gráficos se vuelven más complejos, ya que permite interactuar con cualquier sección del gráfico de forma directa a través de su variable sin importar el orden.





<hr>

