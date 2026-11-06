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


# Valores nulos en Python


En Python, la representación y el manejo de los valores nulos dependen del entorno en el que estés trabajando: el entorno nativo de Python o el análisis de datos con librerías como Pandas y NumPy.
En Python puro, el valor nulo se representa con la palabra clave None, mientras que en ciencia de datos se utiliza NaN (Not a Number) para gestionar datos faltantes en estructuras numéricas o tablas.



## 1. Python Puro: None

None es un objeto especial de tipo NoneType que indica la ausencia de valor o que una variable está vacía.
* Cómo verificarlo: Siempre se debe evaluar utilizando el operador de identidad is o is not.
````
variable = None

if variable is None:
    print("La variable es nula")

if variable is not None:
    print("La variable tiene un valor")
````


## 2. Ciencia de Datos: NaN (Pandas y NumPy)

Cuando trabajas con tablas de datos (DataFrames), los valores nulos numéricos se representan como NaN (un tipo especial de float). Para gestionarlos eficientemente, las herramientas principales son las siguientes:

Detección de nulos

Para saber cuántos datos faltan en un conjunto de datos, se combinan funciones de detección con sumatorias:
````
import pandas as pd
import numpy as np

# Crear un DataFrame de ejemplo
data = {'Nombre': ['Ana', 'Luis', 'Carlos'], 'Edad': [23, np.nan, 31]}
df = pd.DataFrame(data)

# Detectar nulos (devuelve True/False)
print(df.isna())  # O también df.isnull()

# Contar cuántos nulos hay por cada columna
print(df.isna().sum())
````



### Limpieza y tratamiento de nulos

Una vez identificados, existen dos estrategias principales para solucionar la falta de datos:
* Eliminar las filas con nulos (dropna): Borra cualquier fila que contenga al menos un valor vacío.
````
df_limpio = df.dropna()
````

* Reemplazar o imputar los nulos (fillna): Rellena los espacios vacíos con un valor fijo, con la media de la columna o con métodos de propagación.

#### Rellenar con un valor específico (ej. cero o un texto)
````
df['Edad'] = df['Edad'].fillna(0)
````
#### Rellenar con la media de esa columna
````
df['Edad'] = df['Edad'].fillna(df['Edad'].mean())
````



# Tratamiento de Datos Nulos

Los datos del mundo real rara vez son limpios y homogéneos; suelen contener datos faltantes conocidos genéricamente como valores nulos, missing, NaN o NA.

## 1. Estrategias Generales para Datos Faltantes

Existen dos enfoques principales en la programación para representar la ausencia de datos:
* Máscaras: Matrices booleanas independientes o bits locales dedicados a indicar globalmente si un valor es nulo. Añaden sobrecarga de almacenamiento y cálculo.
* Valores Centinela: Convenciones específicas de los datos (como usar -9999) o globales como NaN (Not a Number). Reducen el rango de valores válidos y no están disponibles para todos los tipos de datos. El lenguaje R, por ejemplo, usa centinelas integrados por cada tipo de dato.

## 2. El Enfoque de Pandas

Debido a que NumPy no tiene soporte nativo de valores NA para tipos no flotantes, Pandas optó por un compromiso y adoptó dos centinelas existentes en Python:
* None (Faltante Pythonico): Es un objeto singleton de Python. Solo se puede usar en arrays de tipo object. Genera mucha sobrecarga computacional en comparación con los tipos nativos y produce errores (TypeError) al intentar realizar operaciones aritméticas o agregaciones (como .sum()).
* NaN (Faltante Numérico): Es un valor especial de punto flotante estándar (IEEE). Permite operaciones rápidas en código compilado, pero actúa como un "virus": cualquier operación aritmética con un NaN da como resultado otro NaN.

Conversión Automática (Upcasting)

Pandas gestiona ambos de forma casi intercambiable. Si introduces un nulo en un tipo de dato que no lo admite nativamente, Pandas realiza una conversión automática:
````
Clase de Tipo	        	Conversión al almacenar un NA		Valor Centinela NA
floating (Decimales)		Sin cambios	                    	np.nan
object (Objetos/Strings)	Sin cambios	                    	None o np.nan
integer (Enteros)	        Convierte a float64	            	np.nan
boolean (Booleanos)	        Convierte a object	            	None o np.nan
````
Nota: Los datos de texto (cadenas/strings) siempre se guardan con el dtype object.

## 3. Funciones Principales para Operar con Nulos


### A. Detección

* isnull(): Genera una máscara booleana devolviendo True donde hay un valor nulo.
* notnull(): Lo opuesto a isnull(), devuelve True en las posiciones con datos válidos. Las máscaras booleanas se pueden usar directamente para filtrar las estructuras de datos.

### B. Eliminación (dropna)

Permite filtrar y descartar los datos nulos. En un DataFrame, al no poder borrarse celdas individuales, se eliminan filas o columnas completas mediante parámetros:
* axis: Por defecto es 0 o 'rows' (elimina filas); configurado en 1 o 'columns' elimina las columnas que tengan nulos.
* how: Determina el criterio de borrado. Por defecto es 'any' (borra si hay al menos un nulo). Puede cambiarse a 'all' para borrar solo si toda la fila/columna es nula.
* thresh: Permite establecer de forma precisa un número mínimo de valores no nulos requeridos para conservar la fila o columna.

### C. Reemplazo e Imputación (fillna)

Devuelve una copia de la estructura con los valores nulos reemplazados:
* Valor fijo: Rellenar con un escalar como el cero (df.fillna(0)) o con estadísticos estadísticos de una columna (df.fillna(df[1].mean())).
* Propagación: Rellenar según la posición de otros datos usando el parámetro method:
	* ffill (forward-fill): Propaga el último valor válido hacia adelante.
	* bfill (back-fill): Propaga el siguiente valor válido hacia atrás. (También se puede parametrizar el sentido de la propagación con el argumento axis).


<hr>




# Agregación y Agrupación en Pandas

El análisis eficiente de grandes volúmenes de datos requiere la capacidad de sumarizar, es decir, reducir múltiples registros a un único valor descriptivo mediante operaciones estadísticas.

## 1. Agregación Básica en Pandas

Las agregaciones devuelven un único valor en una Series, pero en un DataFrame calculan el resultado para cada columna de forma independiente.
* Modificación de eje: El argumento axis='columns' permite realizar la agregación de manera horizontal (por filas).
* Método describe(): Computa de forma automática las estadísticas descriptivas estándar para entender las propiedades generales de un conjunto de datos (conteo, media, desviación estándar, mínimo, máximos y percentiles).

Principales funciones de agregación disponibles:
````
Agregación          Descripción

count()	            Número total de elementos (excluye nulos).
first(), last()     Primer y último elemento del conjunto.
mean(), median()    Media aritmética y mediana.
min(), max()	    Valores mínimo y máximo.
std(), var()	    Desviación estándar y varianza.
mad()	            Desviación media absoluta.
prod()	            Producto de todos los elementos.
sum()	            Suma de todos los elementos.
````

## 2. GroupBy: Split, Apply, Combine

Para agrupaciones condicionales basadas en dimensiones o índices, se utiliza el proceso matemático conocido como Split-Apply-Combine:
1. Split (Separar): Rompe y agrupa el DataFrame dependiendo del valor de una clave.
2. Apply (Aplicar): Computa una función (agregación, transformación o filtrado) dentro de cada grupo individual.
3. Combine (Combinar): Une los resultados de los grupos en un único objeto o matriz de salida.
* Evaluación perezosa (Lazy Evaluation): Al invocar .groupby(), Pandas no realiza ningún cálculo inmediatamente, sino que devuelve un objeto DataFrameGroupBy (una vista especial) que espera la instrucción de qué agregación aplicar.

El Objeto GroupBy soporta:

* Indexado de columnas: Seleccionar una columna específica tras agrupar (ej. df.groupby('key')['col'].mean()).
* Iteración directa: Permite recorrer manualmente los grupos mediante bucles for (retornando el nombre del grupo y su sub-DataFrame correspondiente).
* Métodos de envío: Cualquier método válido de un DataFrame (como .describe()) se puede encadenar a un objeto agrupado para ejecutarse de forma aislada en cada grupo.

## 3. Operaciones avanzadas: Aggregate, Filter, Transform y Apply

Más allá de las sumas o medias simples, existen métodos para procesar grupos con mayor flexibilidad:
* aggregate() / agg(): Permite calcular múltiples funciones estadísticas a la vez pasando cadenas, listas de funciones o un diccionario que asocie columnas con operaciones específicas.
* filter(): Descarta o mantiene grupos enteros en función de una propiedad booleana evaluada sobre el grupo completo (ej. filtrar grupos cuyo valor mínimo supere un umbral).
* transform(): Devuelve una versión modificada de los datos que tiene la misma forma exacta (dimensiones) que el DataFrame original. Se usa comúnmente para normalizar o centrar datos restando la media del grupo.
* apply(): Permite aplicar una función arbitraria a los sub-DataFrames de cada grupo. El resultado se combina automáticamente adaptándose a lo que devuelva la función (escalares, Series o DataFrames).

Opciones para especificar las llaves de separación:

Los grupos no solo se definen por nombres de columnas; también pueden agruparse mediante:
* Una lista o array externo con la misma longitud que el DataFrame.
* Un diccionario o serie que mapee los índices actuales a nuevos nombres de grupos.
* Cualquier función nativa de Python (como str.lower para normalizar cadenas del índice).
* Una lista combinada de las opciones anteriores para generar multi-índices (índices jerárquicos).

## 4. Pivot Tables (Tablas Dinámicas)

Son conceptualmente versiones multidimensionales de la agregación GroupBy. Mientras que GroupBy divide y combina datos sobre un eje unidimensional, la tabla dinámica lo hace distribuyendo los datos en una cuadrícula bidimensional.

Sintaxis y argumentos principales:

````
df.pivot_table(data, values=None, index=None, columns=None,
               aggfunc='mean', fill_value=None, margins=False,
               dropna=True, margins_name='All')
````

* index y columns: Definen qué variables se colocarán en las filas y en las columnas de la cuadrícula.
* aggfunc: Controla el tipo de agregación (por defecto es 'mean'). Puede recibir diccionarios para aplicar funciones distintas a cada columna.
* margins=True: Añade automáticamente filas y columnas de totales globales y subtotales (etiquetados por defecto como "All").
* Multi-nivel: Se pueden pasar listas a index o columns (combinadas con funciones como pd.cut o pd.qcut para agrupar por rangos o cuantiles) para construir resúmenes de más de dos dimensiones.



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

