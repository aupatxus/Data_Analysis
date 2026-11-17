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







# 📊 MATPLOTLIB: GRÁFICOS DE LÍNEAS, SCATTER PLOTS Y PERSONALIZACIÓN DE LEYENDAS

# 1. INTRODUCCIÓN A MATPLOTLIB

Matplotlib es una biblioteca de Python utilizada para crear visualizaciones de datos. Permite representar información mediante diferentes tipos de gráficos y personalizar prácticamente todos sus elementos visuales.

En este tema se estudian tres aspectos fundamentales:

1. **Simple Line Plots:** creación y personalización de gráficos de líneas.
2. **Simple Scatter Plots:** creación de gráficos de dispersión y representación de datos multidimensionales.
3. **Personalización de leyendas:** configuración de leyendas, selección de elementos y creación de leyendas múltiples.

## 1.1. Importación de bibliotecas

Para trabajar con Matplotlib, NumPy y Pandas, se importan las siguientes bibliotecas:

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

plt.style.use('seaborn-v0_8')
```

- `matplotlib.pyplot`: proporciona las funciones necesarias para crear y personalizar gráficos.
- `numpy`: permite generar y manipular datos numéricos.
- `pandas`: facilita la lectura y manipulación de conjuntos de datos.
- `plt.style.use()`: permite establecer un estilo visual predeterminado para los gráficos.

También puede utilizarse:

```python
# %matplotlib inline
```

En los notebooks de Jupyter, esta instrucción permite mostrar los gráficos directamente dentro del notebook.

---

# 2. SIMPLE LINE PLOTS: GRÁFICOS DE LÍNEAS

Un gráfico de líneas es una de las representaciones gráficas más sencillas y utilizadas.

Permite representar una función matemática de la forma:

$$
y = f(x)
$$

En este tipo de gráfico:

- El eje X representa los valores de entrada.
- El eje Y representa los valores correspondientes de la función.
- Los puntos se conectan mediante segmentos de línea.

Son especialmente útiles para visualizar funciones matemáticas, tendencias, evoluciones temporales y relaciones entre variables.

## 2.1. Conceptos fundamentales: Figure y Axes

En Matplotlib, la creación de gráficos se basa principalmente en dos objetos:

### Figure (`fig`)

La figura es el contenedor principal de la visualización.

Es una instancia de la clase `plt.Figure` y contiene todos los elementos que forman el gráfico:

- Los ejes.
- Los gráficos.
- Los textos.
- Los títulos.
- Las etiquetas.
- Las leyendas.

Una figura puede contener uno o varios sistemas de ejes.

### Axes (`ax`)

Los ejes son el espacio concreto donde se representa la información.

Es una instancia de la clase `plt.Axes` y contiene:

- Los puntos y las líneas.
- Los ejes X e Y.
- Las etiquetas.
- Los títulos.
- Los elementos visuales del gráfico.

**Diferencia fundamental:**

- `Figure`: representa el contenedor general de la visualización.
- `Axes`: representa el área donde se dibujan los datos.

Por convención, se utilizan las variables:

```python
fig  # Figura.
ax   # Ejes.
```

## 2.2. Creación de una figura y unos ejes

La forma más básica de crear una figura y unos ejes es:

```python
fig = plt.figure()
ax = plt.axes()
```

También se pueden crear conjuntamente:

```python
fig, ax = plt.subplots()
```

Una vez creados los ejes, se pueden representar los datos mediante `ax.plot()`.

## 2.3. Representación de una función matemática

Para representar una función seno, primero generamos los valores del eje X utilizando NumPy.

```python
x = np.linspace(0, 10, 1000)

y = np.sin(x)

fig = plt.figure()
ax = plt.axes()

ax.plot(x, y);
```

### Función `np.linspace()`

Permite generar una secuencia de números distribuidos uniformemente dentro de un intervalo.

Sintaxis:

```python
np.linspace(inicio, final, numero_elementos)
```

Ejemplo:

```python
x = np.linspace(0, 10, 1000)
```

Genera 1000 valores comprendidos entre 0 y 10.

### Función `np.sin()`

Calcula el seno de los valores proporcionados.

```python
y = np.sin(x)
```

De esta manera, obtenemos los valores necesarios para representar:

$$
y = \sin(x)
$$

### Método `ax.plot()`

Permite representar los datos sobre unos ejes concretos.

```python
ax.plot(x, y)
```

Recibe principalmente dos argumentos:

- `x`: valores del eje horizontal.
- `y`: valores del eje vertical.

Ambos conjuntos deben tener dimensiones compatibles.

## 2.4. Interfaz pyplot frente a interfaz orientada a objetos

Matplotlib permite trabajar utilizando dos interfaces diferentes.

### A. Interfaz orientada a objetos

Consiste en crear explícitamente una figura y unos ejes y utilizar sus métodos.

```python
fig = plt.figure()
ax = plt.axes()

ax.plot(x, np.sin(x))
```

También puede utilizarse:

```python
fig, ax = plt.subplots()

ax.plot(x, np.sin(x))
```

En este enfoque, las operaciones se realizan directamente sobre el objeto `ax`.

Es una alternativa especialmente útil cuando se trabaja con gráficos complejos o con varias figuras y ejes.

### B. Interfaz pyplot o estilo MATLAB

También podemos utilizar directamente las funciones de `matplotlib.pyplot`.

```python
plt.plot(x, np.sin(x))
```

En este caso, Matplotlib crea automáticamente la figura y los ejes necesarios en segundo plano.

No necesitamos crear previamente los objetos `fig` y `ax`.

### Comparación

| Interfaz | Ejemplo | Característica |
|---|---|---|
| Orientada a objetos | `ax.plot(x, y)` | Trabaja directamente sobre unos ejes concretos. |
| Pyplot | `plt.plot(x, y)` | Utiliza los ejes actuales y crea los elementos necesarios automáticamente. |

Ambas interfaces permiten crear gráficos, pero la interfaz orientada a objetos ofrece un control más explícito sobre las figuras y sus ejes.

## 2.5. Representación de múltiples líneas

Para representar varias funciones dentro de un mismo gráfico, basta con ejecutar varias llamadas a `plot()`.

Por ejemplo:

```python
plt.plot(x, np.sin(x))
plt.plot(x, np.cos(x))
```

Esto representa simultáneamente:

$$
y_1 = \sin(x)
$$

$$
y_2 = \cos(x)
$$

También podemos utilizar la interfaz orientada a objetos:

```python
fig, ax = plt.subplots()

ax.plot(x, np.sin(x))
ax.plot(x, np.cos(x))
```

Cada llamada añade una nueva línea al mismo sistema de ejes.

---

# 3. PERSONALIZACIÓN DE LOS GRÁFICOS DE LÍNEAS

Matplotlib permite modificar la apariencia de las líneas mediante argumentos adicionales de la función `plot()`.

Los principales aspectos que se pueden personalizar son:

- El color.
- El estilo de línea.
- Los límites de los ejes.
- Los títulos.
- Las etiquetas.
- Las leyendas.

## 3.1. Personalización del color de las líneas

El argumento `color` permite establecer el color de una línea.

```python
plt.plot(x, np.sin(x), color='blue')
```

Matplotlib admite diferentes formas de especificar los colores.

### A. Nombre del color

Se puede utilizar directamente el nombre del color.

```python
plt.plot(x, np.sin(x), color='blue')
plt.plot(x, np.sin(x), color='red')
plt.plot(x, np.sin(x), color='green')
```

### B. Códigos abreviados

Se pueden utilizar códigos de una sola letra.

| Código | Color |
|---|---|
| `b` | Blue (azul) |
| `g` | Green (verde) |
| `r` | Red (rojo) |
| `c` | Cyan (cian) |
| `m` | Magenta |
| `y` | Yellow (amarillo) |
| `k` | Black (negro) |
| `w` | White (blanco) |

Ejemplo:

```python
plt.plot(x, np.sin(x), color='g')
```

### C. Escala de grises

Se puede especificar un número entre 0 y 1 como cadena.

```python
plt.plot(x, np.sin(x), color='0.75')
```

- `0`: negro.
- `1`: blanco.
- Valores intermedios: diferentes tonalidades de gris.

### D. Código hexadecimal

También se pueden utilizar códigos hexadecimales RGB.

```python
plt.plot(x, np.sin(x), color='#25B12F')
```

El formato es:

```text
#RRGGBB
```

Cada componente representa la intensidad de rojo, verde y azul.

### E. Tupla RGB

Se puede especificar el color mediante una tupla de tres valores.

```python
plt.plot(
    x,
    np.sin(x),
    color=(1.0, 0.2, 0.3)
)
```

Cada componente RGB toma valores entre 0 y 1.

### F. Nombres de colores HTML

Matplotlib también admite nombres de colores HTML.

```python
plt.plot(x, np.sin(x), color='chartreuse')
```

### Colores automáticos

Si no se especifica el color, Matplotlib utiliza automáticamente una secuencia de colores predeterminada para diferenciar las distintas líneas de un gráfico.

## 3.2. Personalización del estilo de línea

El argumento `linestyle` permite modificar el patrón de la línea.

Los cuatro estilos principales son:

| Nombre | Código largo | Código corto |
|---|---|---|
| Línea continua | `'solid'` | `'-'` |
| Línea discontinua | `'dashed'` | `'--'` |
| Línea de puntos y rayas | `'dashdot'` | `'-.'` |
| Línea de puntos | `'dotted'` | `':'` |

Ejemplo:

```python
plt.plot(x, x + 0, linestyle='solid')
plt.plot(x, x + 1, linestyle='dashed')
plt.plot(x, x + 2, linestyle='dashdot')
plt.plot(x, x + 3, linestyle='dotted')
```

También se pueden utilizar los códigos abreviados:

```python
plt.plot(x, x + 4, linestyle='-')
plt.plot(x, x + 5, linestyle='--')
plt.plot(x, x + 6, linestyle='-.')
plt.plot(x, x + 7, linestyle=':')
```

## 3.3. Combinar color y estilo de línea

Matplotlib permite combinar el color y el estilo en un único argumento posicional.

Esto permite escribir código más compacto.

```python
plt.plot(x, x + 0, '-r')
plt.plot(x, x + 1, '--c')
plt.plot(x, x + 2, '-.k')
plt.plot(x, x + 3, ':r')
```

La estructura general es:

```python
plt.plot(x, y, estilo_color)
```

Por ejemplo:

- `'-r'`: línea continua roja.
- `'--c'`: línea discontinua cian.
- `'-.k'`: línea de puntos y rayas negra.
- `':r'`: línea de puntos roja.

Los códigos de color de un solo carácter utilizan las abreviaturas habituales de los sistemas RGB y CMYK.

---

# 4. AJUSTAR LOS GRÁFICOS: LÍMITES DE LOS EJES

Matplotlib calcula automáticamente los límites de los ejes para mostrar los datos.

Sin embargo, en ocasiones necesitamos controlar manualmente el intervalo visible.

Para ello existen varias funciones.

## 4.1. Función `plt.xlim()`

Permite establecer los límites del eje horizontal.

Sintaxis:

```python
plt.xlim(valor_minimo, valor_maximo)
```

Ejemplo:

```python
plt.plot(x, np.sin(x))

plt.xlim(-1, 11)
```

El eje X mostrará el intervalo comprendido entre -1 y 11.

## 4.2. Función `plt.ylim()`

Permite establecer los límites del eje vertical.

Sintaxis:

```python
plt.ylim(valor_minimo, valor_maximo)
```

Ejemplo:

```python
plt.plot(x, np.sin(x))

plt.ylim(-1.5, 1.5)
```

El eje Y mostrará el intervalo comprendido entre -1.5 y 1.5.

### Ejemplo conjunto

```python
plt.plot(x, np.sin(x))

plt.xlim(-1, 11)
plt.ylim(-1.5, 1.5)
```

## 4.3. Invertir los ejes

También es posible invertir el sentido de representación de cualquiera de los ejes.

Para ello, basta con proporcionar los límites en orden inverso.

```python
plt.plot(x, np.sin(x))

plt.xlim(5, 0)
plt.ylim(1.2, -1.2)
```

En este ejemplo:

- El eje X se representa desde 5 hasta 0.
- El eje Y se representa desde 1.2 hasta -1.2.

Por tanto, el orden de los argumentos determina también el sentido de representación.

## 4.4. Función `plt.axis()`

La función `plt.axis()` permite controlar simultáneamente los límites de los dos ejes.

Su sintaxis es:

```python
plt.axis([xmin, xmax, ymin, ymax])
```

Ejemplo:

```python
plt.plot(x, np.sin(x))

plt.axis([-1, 11, -1.5, 1.5])
```

El orden de los valores es importante:

1. Límite mínimo del eje X.
2. Límite máximo del eje X.
3. Límite mínimo del eje Y.
4. Límite máximo del eje Y.

### A. Ajuste automático: `tight`

Permite ajustar los límites alrededor del contenido del gráfico.

```python
plt.plot(x, np.sin(x))

plt.axis('tight')
```

Matplotlib adapta los límites para que se ajusten estrechamente a los datos representados.

### B. Relación de aspecto igual: `equal`

Permite establecer una relación de aspecto igual entre los ejes.

```python
plt.plot(x, np.sin(x))

plt.axis('equal')
```

Esto garantiza que una unidad del eje X tenga la misma longitud visual que una unidad del eje Y.

Es especialmente útil cuando interesa preservar las proporciones geométricas de los datos.

### Resumen de las funciones de límites

| Función | Utilidad |
|---|---|
| `plt.xlim()` | Modifica los límites del eje X. |
| `plt.ylim()` | Modifica los límites del eje Y. |
| `plt.axis()` | Modifica simultáneamente los límites de ambos ejes. |
| `plt.axis('tight')` | Ajusta los límites alrededor de los datos. |
| `plt.axis('equal')` | Establece una relación de aspecto igual. |

---

# 5. ETIQUETADO DE LOS GRÁFICOS

Para interpretar correctamente una visualización es importante añadir información descriptiva.

Matplotlib permite incorporar:

- Títulos.
- Etiquetas del eje X.
- Etiquetas del eje Y.
- Leyendas.

## 5.1. Función `plt.title()`

Permite establecer el título del gráfico.

```python
plt.title("A sin curve")
```

El título proporciona una descripción general de la información representada.

## 5.2. Función `plt.xlabel()`

Permite establecer el nombre del eje horizontal.

```python
plt.xlabel("Valores")
```

## 5.3. Función `plt.ylabel()`

Permite establecer el nombre del eje vertical.

```python
plt.ylabel("y")
```

### Ejemplo completo

```python
plt.plot(x, np.sin(x))

plt.title("A sin curve")
plt.xlabel("Valores")
plt.ylabel("y")

plt.xlim(0, 20)
```

### Personalización de las etiquetas

La posición, el tamaño y el estilo de los títulos y las etiquetas pueden modificarse mediante argumentos opcionales.

Para conocer todas las posibilidades se puede consultar la documentación y los docstrings de las funciones correspondientes.

---

# 6. LEYENDAS BÁSICAS

Cuando un gráfico contiene varias líneas, es importante identificar qué representa cada una.

Para ello utilizamos las leyendas.

## 6.1. Función `plt.legend()`

Permite mostrar una leyenda que identifica los distintos elementos del gráfico.

La forma más sencilla de utilizarla consiste en asignar previamente una etiqueta a cada línea mediante el argumento `label`.

```python
plt.plot(
    x,
    np.sin(x),
    '-g',
    label='sin(x)'
)

plt.plot(
    x,
    np.cos(x),
    ':b',
    label='cos(x)'
)

plt.legend()
```

Matplotlib utiliza las etiquetas proporcionadas para construir automáticamente la leyenda.

Además, conserva la correspondencia entre:

- El color de cada línea.
- El estilo de cada línea.
- El texto descriptivo correspondiente.

De esta manera, cada etiqueta aparece asociada visualmente a su línea.

---

# 7. TRANSICIÓN ENTRE LA INTERFAZ PYPLOT Y LA INTERFAZ ORIENTADA A OBJETOS

Matplotlib permite utilizar las funciones de `plt` o los métodos de los objetos `ax`.

Muchas funciones tienen una equivalencia directa.

Sin embargo, algunas funciones de etiquetas, títulos y límites cambian ligeramente de nombre.

La correspondencia es la siguiente:

| Interfaz pyplot | Interfaz orientada a objetos |
|---|---|
| `plt.xlabel()` | `ax.set_xlabel()` |
| `plt.ylabel()` | `ax.set_ylabel()` |
| `plt.xlim()` | `ax.set_xlim()` |
| `plt.ylim()` | `ax.set_ylim()` |
| `plt.title()` | `ax.set_title()` |
| `plt.plot()` | `ax.plot()` |
| `plt.legend()` | `ax.legend()` |

## 7.1. Método `ax.set()`

En lugar de modificar cada propiedad de los ejes mediante una llamada independiente, podemos utilizar el método `ax.set()`.

Este método permite establecer varias propiedades simultáneamente.

Ejemplo:

```python
fig, ax = plt.subplots()

ax.plot(x, np.sin(x))

ax.set(
    xlim=(0, 10),
    ylim=(-2, 2),
    xlabel='x',
    ylabel='sin(x)',
    title='A Simple Plot'
)
```

En una única llamada podemos establecer:

- `xlim`: límites del eje X.
- `ylim`: límites del eje Y.
- `xlabel`: etiqueta del eje X.
- `ylabel`: etiqueta del eje Y.
- `title`: título del gráfico.

Es una forma más compacta de personalizar los ejes cuando utilizamos la interfaz orientada a objetos.

---

# 8. SIMPLE SCATTER PLOTS: GRÁFICOS DE DISPERSIÓN

Un gráfico de dispersión (*scatter plot*) es un tipo de visualización relacionado con los gráficos de líneas.

La principal diferencia es que los puntos no están conectados mediante segmentos de línea.

Cada observación se representa individualmente mediante un símbolo, como:

- Un punto.
- Un círculo.
- Una cruz.
- Un triángulo.
- Un cuadrado.

Los gráficos de dispersión permiten observar relaciones, distribuciones y patrones entre variables.

Matplotlib proporciona principalmente dos formas de crear gráficos de dispersión:

1. Utilizando `plt.plot()`.
2. Utilizando `plt.scatter()`.

---

# 9. CREAR SCATTER PLOTS CON `plt.plot()`

Aunque `plt.plot()` se utiliza habitualmente para crear gráficos de líneas, también permite representar puntos individuales.

Para ello se utilizan los códigos de marcadores.

Ejemplo:

```python
x = np.linspace(0, 10, 50)
y = np.sin(x)

plt.plot(x, y, '-ok', color='black')
```

En este caso:

- `x`: coordenadas horizontales.
- `y`: coordenadas verticales.
- `o`: marcador circular.
- `-`: línea continua.
- `k`: código de color negro.

Los marcadores permiten controlar cómo se representa cada observación.

## 9.1. Tipos de marcadores

Matplotlib dispone de numerosos códigos para representar los puntos.

Algunos de los más utilizados son:

| Código | Marcador |
|---|---|
| `'o'` | Círculo |
| `'.'` | Punto |
| `','` | Pixel |
| `'x'` | Cruz |
| `'+'` | Signo más |
| `'v'` | Triángulo hacia abajo |
| `'^'` | Triángulo hacia arriba |
| `'<'` | Triángulo hacia la izquierda |
| `'>'` | Triángulo hacia la derecha |
| `'s'` | Cuadrado |
| `'d'` | Diamante |

Ejemplo:

```python
rng = np.random.RandomState()

for marker in ['o', '.', ',', 'x', '+',
               'v', '^', '<', '>', 's', 'd']:

    plt.plot(
        rng.rand(5),
        rng.rand(5),
        marker,
        label="marker='{0}'".format(marker)
    )

plt.legend(numpoints=1)
plt.xlim(0, 1.8)
```

En este ejemplo:

- `np.random.RandomState()` permite generar números aleatorios.
- `rng.rand(5)` genera cinco valores aleatorios.
- El bucle recorre diferentes tipos de marcadores.
- `label` permite identificar cada tipo de marcador.
- `plt.legend()` muestra la leyenda.
- `numpoints=1` establece que la leyenda muestre un único punto por entrada.

## 9.2. Combinar líneas y marcadores

Los códigos de marcadores pueden combinarse con los códigos de color y de estilo de línea.

```python
plt.plot(x, y, '-ok')
```

Esto permite representar simultáneamente:

- Los puntos individuales.
- Una línea que conecta los puntos.
- Un estilo visual determinado.

## 9.3. Personalización avanzada de líneas y marcadores

La función `plt.plot()` admite argumentos adicionales para controlar las propiedades visuales.

Los más importantes que aparecen en el notebook son:

### `color`

Establece el color de la línea y, en general, el color asociado al trazado.

```python
color='gray'
```

### `linewidth`

Controla el grosor de la línea.

```python
linewidth=10
```

### `markersize`

Controla el tamaño de los marcadores.

```python
markersize=15
```

### `markerfacecolor`

Establece el color interior de los marcadores.

```python
markerfacecolor='blue'
```

### `markeredgecolor`

Establece el color del borde de los marcadores.

```python
markeredgecolor='black'
```

### `markeredgewidth`

Controla el grosor del borde de los marcadores.

```python
markeredgewidth=2
```

### Ejemplo completo

```python
plt.plot(
    x,
    y,
    '-ok',
    color='gray',
    linewidth=10,
    markersize=15,
    markerfacecolor='blue',
    markeredgecolor='black',
    markeredgewidth=2
)
```

Este conjunto de argumentos permite personalizar tanto las líneas como los puntos que forman el gráfico.

---

# 10. CREAR SCATTER PLOTS CON `plt.scatter()`

Otra forma de crear gráficos de dispersión consiste en utilizar la función `plt.scatter()`.

Su funcionamiento básico es muy similar al de `plt.plot()`.

```python
plt.scatter(x, y)
```

Esta función representa cada observación como un punto independiente.

## 10.1. Diferencia fundamental entre `plt.plot()` y `plt.scatter()`

La principal diferencia es la capacidad de personalización individual de cada punto.

Con `plt.scatter()` podemos modificar individualmente propiedades como:

- El tamaño.
- El color interior.
- El color del borde.
- La transparencia.

Además, estas propiedades pueden asignarse directamente a variables del conjunto de datos.

Esto permite representar más información dentro de un único gráfico.

## 10.2. Argumentos principales de `plt.scatter()`

### `x`

Contiene las coordenadas horizontales de los puntos.

### `y`

Contiene las coordenadas verticales de los puntos.

### `c`

Permite especificar el color de los puntos.

Puede recibir un color fijo o valores numéricos que se traducen en una escala de colores.

```python
c=colors
```

### `s`

Permite establecer el tamaño de los puntos.

Puede utilizarse un valor fijo o un conjunto de valores que determine el tamaño individual de cada observación.

```python
s=sizes
```

El tamaño se expresa en puntos cuadrados de área (points²).

### `alpha`

Controla la transparencia de los elementos.

Sus valores habituales se encuentran entre 0 y 1:

- `alpha=0`: completamente transparente.
- `alpha=0.5`: transparencia intermedia.
- `alpha=1`: completamente opaco.

Ejemplo:

```python
alpha=0.8
```

### `cmap`

Permite seleccionar el mapa de colores utilizado para traducir los valores numéricos de `c` a colores.

Ejemplo:

```python
cmap='viridis'
```

### `plt.colorbar()`

Permite mostrar una barra de colores que explica la correspondencia entre los valores numéricos y los colores utilizados.

---

# 11. SCATTER PLOTS CON TAMAÑOS Y COLORES VARIABLES

Una de las grandes ventajas de `plt.scatter()` es que permite representar varias dimensiones de información simultáneamente.

Ejemplo:

```python
rng = np.random.RandomState(0)

x = rng.randn(100)
y = rng.randn(100)

colors = rng.rand(100)
sizes = 1000 * rng.rand(100)

plt.scatter(
    x,
    y,
    c=colors,
    s=sizes,
    alpha=0.8,
    cmap='viridis'
)

plt.colorbar()
```

### Explicación del ejemplo

Primero se generan 100 observaciones aleatorias:

```python
x = rng.randn(100)
y = rng.randn(100)
```

Después se generan dos variables adicionales:

```python
colors = rng.rand(100)
sizes = 1000 * rng.rand(100)
```

Estas variables controlan la apariencia de los puntos.

Finalmente:

```python
plt.scatter(
    x,
    y,
    c=colors,
    s=sizes,
    alpha=0.8,
    cmap='viridis'
)
```

Se construye el gráfico de dispersión.

La información se distribuye de la siguiente manera:

| Elemento visual | Información representada |
|---|---|
| Posición horizontal | Variable X |
| Posición vertical | Variable Y |
| Color | Valores de `colors` |
| Tamaño | Valores de `sizes` |
| Transparencia | Nivel de opacidad de los puntos |

La función `plt.colorbar()` permite interpretar los colores utilizados.

**Conclusión:** un scatter plot puede representar más de dos variables simultáneamente, utilizando la posición, el tamaño y el color de los puntos.

Esto resulta especialmente útil para visualizar conjuntos de datos multidimensionales.

---

# 12. EJEMPLO PRÁCTICO: DATASET IRIS

El notebook utiliza el conjunto de datos Iris de Scikit-Learn para demostrar cómo representar diferentes dimensiones de información mediante un gráfico de dispersión.

## 12.1. ¿Qué es el dataset Iris?

Iris es un conjunto de datos que contiene observaciones de flores pertenecientes a tres especies diferentes.

Para cada muestra se han medido cuatro características:

1. Longitud del sépalo.
2. Anchura del sépalo.
3. Longitud del pétalo.
4. Anchura del pétalo.

Cada muestra pertenece a una de las tres especies de flores.

## 12.2. Cargar el dataset

Primero importamos la función correspondiente:

```python
from sklearn.datasets import load_iris

iris = load_iris()
```

El objeto `iris` contiene los datos, los nombres de las características y las etiquetas de las especies.

## 12.3. Consultar los nombres de las características

```python
iris.feature_names
```

Permite consultar los nombres de las cuatro variables medidas.

## 12.4. Consultar los datos

```python
iris
```

Permite examinar el objeto completo del conjunto de datos.

## 12.5. Consultar las especies

```python
print(iris.target_names)
```

Permite obtener los nombres de las tres especies.

## 12.6. Transponer los datos

```python
features = iris.data.T
```

La matriz original `iris.data` tiene las observaciones organizadas por filas y las características por columnas.

La operación `.T` transpone la matriz.

Así, cada fila de `features` corresponde a una característica.

Podemos acceder a ellas mediante índices:

| Índice | Característica |
|---|---|
| `features[0]` | Longitud del sépalo |
| `features[1]` | Anchura del sépalo |
| `features[2]` | Longitud del pétalo |
| `features[3]` | Anchura del pétalo |

## 12.7. Representación de cuatro dimensiones

```python
features = iris.data.T

plt.scatter(
    features[0],
    features[2],
    alpha=0.5,
    s=100 * features[3],
    c=iris.target,
    cmap='viridis'
)

plt.xlabel(iris.feature_names[0])
plt.ylabel(iris.feature_names[2])

plt.colorbar()
```

### Interpretación del gráfico

Este gráfico representa cuatro dimensiones diferentes:

| Dimensión | Representación |
|---|---|
| Primera dimensión | Posición X: longitud del sépalo. |
| Segunda dimensión | Posición Y: longitud del pétalo. |
| Tercera dimensión | Tamaño del punto: anchura del pétalo. |
| Cuarta dimensión | Color del punto: especie de la flor. |

Por tanto, un único gráfico permite estudiar simultáneamente cuatro variables.

### Importancia de los scatter plots multidimensionales

Los gráficos de dispersión con múltiples colores y tamaños permiten:

- Explorar relaciones entre variables.
- Identificar agrupaciones.
- Diferenciar categorías.
- Detectar patrones.
- Representar información multidimensional.
- Facilitar tanto la exploración como la presentación de datos.

---

# 13. DIFERENCIAS ENTRE `plt.plot()` Y `plt.scatter()`: EFICIENCIA

Aunque ambas funciones permiten representar puntos, existen diferencias importantes en cuanto a rendimiento.

La elección entre `plt.plot()` y `plt.scatter()` depende principalmente de las características del conjunto de datos y del nivel de personalización necesario.

## 13.1. Funcionamiento de `plt.scatter()`

`plt.scatter()` permite modificar individualmente el tamaño y el color de cada punto.

Por tanto, el renderizador debe realizar trabajo adicional para construir y representar cada punto con sus propiedades particulares.

## 13.2. Funcionamiento de `plt.plot()`

En `plt.plot()`, los puntos de un mismo trazado tienen esencialmente las mismas propiedades visuales.

El trabajo de determinar su apariencia se realiza una sola vez para el conjunto de datos.

Por este motivo, su representación puede ser más eficiente.

## 13.3. Comparación

| Característica | `plt.plot()` | `plt.scatter()` |
|---|---|---|
| Gráficos de líneas | Sí | No es su finalidad principal |
| Puntos individuales | Sí | Sí |
| Tamaño individual por punto | No como capacidad principal | Sí |
| Color individual por punto | No como capacidad principal | Sí |
| Personalización multidimensional | Más limitada | Mayor |
| Eficiencia con muchos puntos | Generalmente superior | Puede ser inferior |
| Personalización individual | Limitada | Muy flexible |

## 13.4. ¿Cuál utilizar?

**Utilizar `plt.plot()` cuando:**

- Se quieren representar funciones matemáticas.
- Se necesitan gráficos de líneas.
- Los puntos comparten las mismas propiedades visuales.
- Se trabaja con conjuntos de datos grandes y se prioriza la eficiencia.

**Utilizar `plt.scatter()` cuando:**

- Se quieren representar observaciones independientes.
- Cada punto necesita un tamaño diferente.
- Cada punto necesita un color diferente.
- Se quieren visualizar varias dimensiones de información.

### Conclusión sobre eficiencia

Cuando los conjuntos de datos superan unos pocos miles de puntos, `plt.plot()` puede ser notablemente más eficiente que `plt.scatter()`.

Por tanto, si no necesitamos asignar propiedades visuales individuales a cada punto, es preferible utilizar `plt.plot()` cuando trabajamos con grandes conjuntos de datos.

---

# 14. PERSONALIZACIÓN DE LAS LEYENDAS

Las leyendas permiten interpretar correctamente los diferentes elementos de una visualización.

Su función es asociar cada elemento gráfico con un significado.

Por ejemplo, en un gráfico que contiene dos líneas, una leyenda permite identificar qué línea representa el seno y cuál representa el coseno.

Matplotlib permite personalizar diferentes aspectos de las leyendas:

- Su posición.
- Su marco.
- El número de columnas.
- La transparencia.
- La sombra.
- Los bordes.
- El relleno.
- Los elementos que aparecen.
- Las etiquetas.

## 14.1. Crear una leyenda básica

La función principal es:

```python
plt.legend()
```

En la interfaz orientada a objetos:

```python
ax.legend()
```

La función crea automáticamente una leyenda utilizando los elementos del gráfico que tengan asignado un atributo `label`.

Ejemplo:

```python
x = np.linspace(0, 10, 1000)

fig, ax = plt.subplots()

ax.plot(
    x,
    np.sin(x),
    '-b',
    label='Sine'
)

ax.plot(
    x,
    np.cos(x),
    '--r',
    label='Cosine'
)

ax.axis([0, 4, 0, 3])

ax.legend()
```

Cada línea aparece identificada por su etiqueta.

## 14.2. Personalizar la posición de la leyenda: `loc`

El argumento `loc` permite establecer la posición de la leyenda.

Ejemplo:

```python
ax.legend(loc='upper left')
```

Algunas posiciones habituales son:

| Valor | Posición |
|---|---|
| `'upper left'` | Superior izquierda |
| `'upper right'` | Superior derecha |
| `'lower left'` | Inferior izquierda |
| `'lower right'` | Inferior derecha |
| `'lower center'` | Centro inferior |
| `'upper center'` | Centro superior |
| `'center'` | Centro |

Ejemplo:

```python
ax.legend(
    loc='upper left',
    frameon=True
)
```

## 14.3. Mostrar u ocultar el marco: `frameon`

El argumento `frameon` permite controlar la presencia del marco de la leyenda.

```python
ax.legend(frameon=True)
```

- `True`: muestra el marco.
- `False`: oculta el marco.

Ejemplo:

```python
ax.legend(
    loc='lower center',
    frameon=False
)
```

## 14.4. Número de columnas: `ncol`

El argumento `ncol` permite determinar cuántas columnas tendrá la leyenda.

```python
ax.legend(ncol=2)
```

Ejemplo:

```python
ax.legend(
    loc='lower center',
    frameon=False,
    ncol=2
)
```

Esto permite distribuir horizontalmente las diferentes etiquetas.

## 14.5. Marco redondeado: `fancybox`

Permite utilizar un marco con esquinas redondeadas.

```python
ax.legend(fancybox=True)
```

## 14.6. Transparencia del marco: `framealpha`

Permite establecer el nivel de transparencia del marco.

```python
ax.legend(framealpha=0.1)
```

Los valores se encuentran entre 0 y 1.

- `0`: completamente transparente.
- `1`: completamente opaco.

## 14.7. Añadir sombra: `shadow`

Permite añadir una sombra a la leyenda.

```python
ax.legend(shadow=True)
```

## 14.8. Relleno del marco: `borderpad`

Permite controlar el espacio interior del marco alrededor del contenido de la leyenda.

```python
ax.legend(borderpad=5)
```

### Ejemplo completo de personalización

```python
ax.legend(
    frameon=True,
    ncol=2,
    fancybox=True,
    framealpha=0.1,
    shadow=True,
    borderpad=5
)
```

Estos argumentos permiten adaptar la estética de la leyenda al diseño del gráfico.

---

# 15. SELECCIÓN DE ELEMENTOS PARA LA LEYENDA

Por defecto, Matplotlib incluye en la leyenda todos los elementos del gráfico que tengan asignado un atributo `label`.

Sin embargo, en ocasiones necesitamos seleccionar únicamente algunos elementos.

Existen diferentes formas de controlar qué elementos aparecen.

## 15.1. Utilizar los objetos devueltos por `plt.plot()`

La función `plt.plot()` puede generar varias líneas en una única llamada.

Además, devuelve una lista de objetos de tipo `Line2D`.

Estos objetos representan las líneas creadas.

Ejemplo:

```python
y = np.sin(
    x[:, np.newaxis] +
    np.pi * np.arange(0, 2, 0.5)
)

lines = plt.plot(x, y)
```

La variable `lines` contiene las líneas creadas.

Podemos seleccionar únicamente las que queremos incluir en la leyenda.

```python
plt.legend(
    lines[:2],
    ['first', 'second']
)
```

### Explicación

- `lines`: contiene los objetos correspondientes a las líneas.
- `lines[:2]`: selecciona las dos primeras líneas.
- `['first', 'second']`: proporciona las etiquetas que aparecerán en la leyenda.

Esta técnica permite decidir manualmente qué elementos aparecen.

## 15.2. Utilizar el argumento `label`

En la práctica, suele ser más sencillo asignar directamente una etiqueta a cada elemento que queremos mostrar.

Ejemplo:

```python
plt.plot(
    x,
    y[:, 0],
    label='first'
)

plt.plot(
    x,
    y[:, 1],
    label='second'
)

plt.plot(
    x,
    y[:, 2:]
)

plt.legend(
    framealpha=1,
    frameon=True
)
```

En este ejemplo:

- Las dos primeras líneas tienen etiquetas.
- La tercera llamada no tiene etiqueta.
- La leyenda incluye únicamente los elementos etiquetados.

**Importante:** por defecto, Matplotlib ignora los elementos que no tienen un atributo `label` establecido.

Esta característica permite controlar fácilmente qué información aparece en la leyenda.

---

# 16. CREAR LEYENDAS PARA EL TAMAÑO DE LOS PUNTOS

En ocasiones, una leyenda convencional no es suficiente.

Por ejemplo, cuando utilizamos el tamaño de los puntos para representar una variable, necesitamos explicar qué significa cada tamaño.

Un ejemplo es representar ciudades utilizando:

- Su ubicación geográfica.
- Su población.
- Su superficie.

En este caso:

- La longitud y la latitud determinan la posición.
- El color representa la población.
- El tamaño representa la superficie.

Es necesario crear una leyenda que explique qué significa cada tamaño de punto.

## 16.1. Cargar el conjunto de datos

El notebook utiliza un archivo CSV con información de ciudades de California.

```python
import pandas as pd

cities = pd.read_csv(
    'data/california_cities.csv'
)

cities.head()
```

`pd.read_csv()` permite cargar los datos desde un archivo CSV.

## 16.2. Extraer las variables

```python
lat = cities['latd']
lon = cities['longd']

population = cities['population_total']
area = cities['area_total_km2']
```

Las variables utilizadas son:

| Variable | Significado |
|---|---|
| `lat` | Latitud de las ciudades |
| `lon` | Longitud de las ciudades |
| `population` | Población total |
| `area` | Superficie total en km² |

## 16.3. Crear el gráfico de dispersión

```python
plt.figure(figsize=(20, 10))

plt.scatter(
    lon,
    lat,
    label=None,
    c=np.log10(population),
    cmap='viridis',
    s=area,
    linewidth=0,
    alpha=0.5
)

plt.xlabel('longitude')
plt.ylabel('latitude')

plt.colorbar(
    label='log$_{10}$(population)'
)

plt.clim(3, 7)

plt.title(
    'California Cities: Area and Population'
)
```

### Interpretación de los argumentos

**`lon` y `lat`**

Determinan la posición geográfica de cada ciudad.

- Eje X: longitud.
- Eje Y: latitud.

**`c=np.log10(population)`**

El color representa el logaritmo decimal de la población.

La expresión matemática es:

$$
\log_{10}(population)
$$

**`cmap='viridis'`**

Establece el mapa de colores utilizado.

**`s=area`**

El tamaño de cada punto representa la superficie de la ciudad.

**`linewidth=0`**

Establece el grosor del borde de los puntos en cero.

**`alpha=0.5`**

Establece un nivel de transparencia del 50 %.

**`plt.colorbar()`**

Añade una escala para interpretar los colores.

**`plt.clim(3, 7)`**

Establece los límites de la escala de colores.

**`plt.figure(figsize=(20, 10))`**

Permite establecer las dimensiones de la figura.

---

# 17. CREAR UNA LEYENDA PERSONALIZADA MEDIANTE LISTAS VACÍAS

El problema del ejemplo anterior es que la leyenda convencional no explica automáticamente qué significa cada tamaño de punto.

Queremos que la leyenda muestre círculos de diferentes tamaños asociados a superficies concretas.

Para conseguirlo, podemos crear objetos gráficos auxiliares que no representen datos reales.

La estrategia consiste en utilizar listas vacías.

## 17.1. Crear elementos artificiales para la leyenda

```python
for area in [100, 300, 500]:

    plt.scatter(
        [],
        [],
        c='k',
        alpha=0.3,
        s=area,
        label=str(area) + ' km$^2$'
    )
```

### ¿Qué está ocurriendo?

Se ejecuta un bucle para crear tres elementos:

- Un círculo de tamaño 100.
- Un círculo de tamaño 300.
- Un círculo de tamaño 500.

La característica fundamental es que se utilizan listas vacías:

```python
plt.scatter([], [])
```

Esto permite crear objetos gráficos etiquetados sin añadir observaciones reales al gráfico.

Los objetos creados pueden ser recogidos posteriormente por la función `plt.legend()`.

Por tanto, conseguimos incorporar símbolos a la leyenda que sirven únicamente como referencia visual.

## 17.2. Configurar la leyenda personalizada

```python
plt.legend(
    scatterpoints=1,
    frameon=False,
    labelspacing=1,
    title='City Area'
)
```

### Argumentos utilizados

**`scatterpoints`**

Permite establecer el número de puntos representados en cada entrada de la leyenda.

**`frameon`**

Controla la visualización del marco.

**`labelspacing`**

Permite ajustar el espacio vertical entre las diferentes etiquetas.

**`title`**

Permite establecer un título para la leyenda.

### ¿Por qué funciona esta estrategia?

La leyenda de Matplotlib se construye a partir de objetos gráficos presentes en el gráfico.

Si queremos mostrar un símbolo concreto que no existe entre los datos representados, podemos crear artificialmente un objeto gráfico con las características deseadas.

Al utilizar listas vacías:

```python
plt.scatter([], [], ...)
```

Creamos un objeto etiquetado sin representar observaciones adicionales.

Matplotlib lo reconoce y lo incorpora a la leyenda.

**Esta técnica permite crear leyendas sofisticadas y personalizadas.**

---

# 18. VISUALIZACIÓN DE DATOS GEOGRÁFICOS Y BASEMAP

En el ejemplo de las ciudades de California se representan datos geográficos mediante coordenadas de longitud y latitud.

Sin embargo, el gráfico sería más claro si incluyera los límites del estado y otros elementos geográficos.

El notebook menciona Basemap como una herramienta de Matplotlib para trabajar con datos geográficos.

Basemap permite incorporar elementos cartográficos que ayudan a contextualizar las coordenadas representadas.

Su utilización se plantea como un tema posterior, dedicado específicamente a la representación de datos geográficos.

---

# 19. CREAR MÚLTIPLES LEYENDAS EN UN MISMO GRÁFICO

En ocasiones necesitamos incorporar varias leyendas a un mismo sistema de ejes.

Por ejemplo, podemos querer diferenciar dos grupos de líneas utilizando dos leyendas independientes.

Sin embargo, Matplotlib presenta una limitación en su interfaz estándar.

## 19.1. Limitación de `plt.legend()` y `ax.legend()`

Por defecto, Matplotlib permite mantener una única leyenda estándar por gráfico.

Si ejecutamos dos veces:

```python
ax.legend()
```

La segunda llamada sustituye a la primera.

Por tanto, no es posible crear dos leyendas independientes simplemente llamando dos veces a `ax.legend()`.

## 19.2. Solución: crear objetos Legend manualmente

Para solucionar esta limitación podemos crear un objeto `Legend` desde cero y añadirlo manualmente al gráfico mediante:

```python
ax.add_artist()
```

Esto permite conservar una primera leyenda y añadir una segunda de forma independiente.

## 19.3. Ejemplo completo

```python
fig, ax = plt.subplots()

lines = []

styles = ['-', '--', '-.', ':']

x = np.linspace(0, 10, 1000)

for i in range(4):

    lines += ax.plot(
        x,
        np.sin(x - i * np.pi / 2),
        styles[i],
        color='black'
    )

ax.axis('equal')
```

En este primer bloque:

1. Se crea una figura y unos ejes.
2. Se inicializa una lista vacía llamada `lines`.
3. Se definen cuatro estilos diferentes.
4. Se generan los valores del eje X.
5. Se representan cuatro funciones seno desplazadas.
6. Los objetos de las líneas se almacenan en la lista `lines`.

Las cuatro líneas utilizan los siguientes estilos:

```python
styles = ['-', '--', '-.', ':']
```

## 19.4. Crear la primera leyenda

```python
ax.legend(
    lines[:2],
    ['line A', 'line B'],
    loc='upper right',
    frameon=False
)
```

Se seleccionan las dos primeras líneas.

La primera leyenda identifica:

- `line A`.
- `line B`.

Se coloca en la esquina superior derecha.

## 19.5. Crear la segunda leyenda

```python
from matplotlib.legend import Legend

leg = Legend(
    ax,
    lines[2:],
    ['line C', 'line D'],
    loc='lower right',
    frameon=False
)

ax.add_artist(leg)
```

### Explicación

**Importación de `Legend`**

```python
from matplotlib.legend import Legend
```

Permite crear directamente objetos de tipo leyenda.

**Creación del objeto**

```python
leg = Legend(
    ax,
    lines[2:],
    ['line C', 'line D'],
    loc='lower right',
    frameon=False
)
```

Se crea una segunda leyenda utilizando:

- `ax`: los ejes donde se incorporará la leyenda.
- `lines[2:]`: las dos últimas líneas.
- `['line C', 'line D']`: las etiquetas correspondientes.
- `loc='lower right'`: posición inferior derecha.
- `frameon=False`: sin marco.

**Añadir el objeto al gráfico**

```python
ax.add_artist(leg)
```

Este método añade manualmente el segundo objeto de leyenda al gráfico.

De esta manera, ambas leyendas pueden mantenerse simultáneamente.

## 19.6. Concepto de Artist en Matplotlib

El notebook introduce aquí el concepto de objetos artísticos de bajo nivel (*Artists*).

Los elementos que componen una visualización de Matplotlib son objetos que forman parte de su estructura gráfica.

Las leyendas también son objetos de este tipo.

Cuando utilizamos:

```python
ax.legend()
```

Matplotlib realiza internamente una serie de operaciones:

1. Crea un objeto `Legend`.
2. Guarda el objeto en el atributo `legend_`.
3. Añade la leyenda a la figura durante el proceso de representación.

Por eso, cuando ejecutamos una segunda llamada a `ax.legend()`, se sustituye la leyenda anterior.

La solución consiste en crear directamente otro objeto `Legend` y añadirlo mediante:

```python
ax.add_artist()
```

Esto permite conservar la primera leyenda y añadir otras adicionales.

Para examinar el funcionamiento interno de las funciones se puede utilizar la ayuda de IPython:

```python
ax.legend??
```

Esto permite inspeccionar el código fuente de la función.

---

# 20. RESUMEN GENERAL DE LAS FUNCIONES Y ARGUMENTOS

Esta sección recopila las funciones, métodos y argumentos más importantes estudiados en el notebook.

## 20.1. Creación de gráficos

| Función | Utilidad |
|---|---|
| `plt.figure()` | Crea una figura. |
| `plt.axes()` | Crea unos ejes. |
| `plt.subplots()` | Crea una figura y uno o varios ejes. |
| `plt.plot(x, y)` | Representa líneas o puntos. |
| `ax.plot(x, y)` | Representa datos sobre unos ejes concretos. |
| `plt.scatter(x, y)` | Crea un gráfico de dispersión. |
| `plt.colorbar()` | Añade una escala de colores. |

## 20.2. Personalización de líneas y puntos

| Argumento | Utilidad |
|---|---|
| `color` | Establece el color. |
| `linestyle` | Establece el estilo de línea. |
| `linewidth` | Modifica el grosor de la línea. |
| `marker` | Establece el símbolo de los puntos. |
| `markersize` | Modifica el tamaño de los marcadores. |
| `markerfacecolor` | Modifica el color interior del marcador. |
| `markeredgecolor` | Modifica el color del borde del marcador. |
| `markeredgewidth` | Modifica el grosor del borde. |
| `alpha` | Controla la transparencia. |
| `c` | Establece el color de los puntos en `scatter()`. |
| `s` | Establece el tamaño de los puntos en `scatter()`. |
| `cmap` | Selecciona el mapa de colores. |

## 20.3. Límites y proporciones

| Función | Utilidad |
|---|---|
| `plt.xlim()` | Modifica los límites del eje X. |
| `plt.ylim()` | Modifica los límites del eje Y. |
| `plt.axis()` | Modifica los límites de ambos ejes. |
| `plt.axis('tight')` | Ajusta los límites al contenido. |
| `plt.axis('equal')` | Establece una relación de aspecto igual. |
| `plt.clim()` | Modifica los límites de la escala de colores. |

## 20.4. Títulos y etiquetas

| Función | Utilidad |
|---|---|
| `plt.title()` | Establece el título. |
| `plt.xlabel()` | Establece la etiqueta del eje X. |
| `plt.ylabel()` | Establece la etiqueta del eje Y. |
| `ax.set()` | Modifica varias propiedades de los ejes simultáneamente. |
| `ax.set_title()` | Establece el título mediante la interfaz orientada a objetos. |
| `ax.set_xlabel()` | Establece la etiqueta X mediante la interfaz orientada a objetos. |
| `ax.set_ylabel()` | Establece la etiqueta Y mediante la interfaz orientada a objetos. |

## 20.5. Leyendas

| Función o argumento | Utilidad |
|---|---|
| `plt.legend()` | Crea una leyenda. |
| `ax.legend()` | Crea una leyenda sobre unos ejes concretos. |
| `label` | Asigna una etiqueta a un elemento gráfico. |
| `loc` | Establece la posición de la leyenda. |
| `frameon` | Muestra u oculta el marco. |
| `ncol` | Establece el número de columnas. |
| `fancybox` | Permite utilizar esquinas redondeadas. |
| `framealpha` | Controla la transparencia del marco. |
| `shadow` | Añade una sombra. |
| `borderpad` | Modifica el relleno interior del marco. |
| `scatterpoints` | Establece los puntos mostrados en cada entrada. |
| `labelspacing` | Modifica el espacio entre etiquetas. |
| `title` | Añade un título a la leyenda. |
| `Legend` | Permite crear manualmente un objeto de leyenda. |
| `ax.add_artist()` | Añade manualmente un objeto gráfico a los ejes. |

## 20.6. Funciones complementarias de NumPy y Pandas

| Función | Utilidad |
|---|---|
| `np.linspace()` | Genera valores distribuidos uniformemente. |
| `np.sin()` | Calcula el seno. |
| `np.cos()` | Calcula el coseno. |
| `np.random.RandomState()` | Inicializa un generador de números aleatorios. |
| `rng.rand()` | Genera números aleatorios uniformes. |
| `rng.randn()` | Genera números aleatorios con distribución normal estándar. |
| `np.log10()` | Calcula el logaritmo decimal. |
| `np.arange()` | Genera secuencias de valores. |
| `pd.read_csv()` | Lee datos desde archivos CSV. |
| `.head()` | Muestra las primeras filas de un DataFrame. |
| `.T` | Transpone una matriz o estructura compatible. |

---

# 21. CONCEPTOS FUNDAMENTALES QUE HAY QUE RECORDAR

## 21.1. Figure y Axes

Son los dos objetos fundamentales de Matplotlib.

- `Figure`: contenedor general del gráfico.
- `Axes`: área donde se representan los datos.

## 21.2. `plt.plot()` frente a `plt.scatter()`

La diferencia más importante es la personalización individual de los puntos.

- `plt.plot()`: adecuado para líneas y puntos con propiedades visuales compartidas.
- `plt.scatter()`: adecuado para puntos independientes con tamaños y colores variables.

Además, `plt.plot()` suele ser más eficiente con grandes cantidades de puntos cuando no necesitamos personalización individual.

## 21.3. Personalización de líneas

Los principales argumentos son:

```python
color
linestyle
linewidth
```

## 21.4. Personalización de marcadores

Los principales argumentos son:

```python
marker
markersize
markerfacecolor
markeredgecolor
markeredgewidth
```

## 21.5. Visualización multidimensional

Un scatter plot puede representar simultáneamente varias dimensiones:

- Coordenada X.
- Coordenada Y.
- Tamaño del punto.
- Color del punto.

Esto permite visualizar más información que la que proporcionan exclusivamente los dos ejes.

## 21.6. Leyendas

La función principal es:

```python
plt.legend()
```

Las etiquetas se asignan mediante:

```python
label='nombre'
```

Se pueden personalizar utilizando:

```python
loc
frameon
ncol
fancybox
framealpha
shadow
borderpad
```

## 21.7. Leyendas personalizadas

Se pueden crear elementos artificiales para una leyenda mediante:

```python
plt.scatter([], [], ...)
```

Esta técnica permite representar símbolos que no corresponden a observaciones reales, pero que sirven para explicar las escalas visuales.

## 21.8. Múltiples leyendas

Matplotlib mantiene una única leyenda estándar por gráfico.

Para añadir varias leyendas se puede crear un objeto `Legend` manualmente y utilizar:

```python
ax.add_artist(leg)
```

---

# 22. CHULETA FINAL: EJEMPLOS DE SINTAXIS

## Crear un gráfico de líneas

```python
plt.plot(x, y)
```

## Crear varios gráficos de líneas

```python
plt.plot(x, np.sin(x))
plt.plot(x, np.cos(x))
```

## Crear una figura y unos ejes

```python
fig, ax = plt.subplots()
```

## Cambiar el color

```python
plt.plot(x, y, color='red')
```

## Cambiar el estilo de línea

```python
plt.plot(x, y, linestyle='--')
```

## Combinar color y estilo

```python
plt.plot(x, y, '-r')
```

## Cambiar los límites

```python
plt.xlim(0, 10)
plt.ylim(-1, 1)
```

## Establecer los límites conjuntamente

```python
plt.axis([0, 10, -1, 1])
```

## Ajustar automáticamente los límites

```python
plt.axis('tight')
```

## Establecer una relación de aspecto igual

```python
plt.axis('equal')
```

## Añadir un título

```python
plt.title('Mi gráfico')
```

## Añadir etiquetas

```python
plt.xlabel('Eje X')
plt.ylabel('Eje Y')
```

## Añadir una leyenda

```python
plt.plot(x, y, label='Mi línea')
plt.legend()
```

## Crear un scatter plot

```python
plt.scatter(x, y)
```

## Crear un scatter plot con tamaños y colores variables

```python
plt.scatter(
    x,
    y,
    c=colors,
    s=sizes,
    alpha=0.5,
    cmap='viridis'
)

plt.colorbar()
```

## Personalizar los marcadores

```python
plt.plot(
    x,
    y,
    '-ok',
    markersize=10,
    markerfacecolor='blue',
    markeredgecolor='black',
    markeredgewidth=2
)
```

## Personalizar una leyenda

```python
plt.legend(
    loc='upper left',
    frameon=True,
    ncol=2,
    fancybox=True,
    framealpha=0.5,
    shadow=True
)
```

## Seleccionar elementos de la leyenda

```python
lines = plt.plot(x, y)

plt.legend(
    lines[:2],
    ['first', 'second']
)
```

## Crear elementos auxiliares para una leyenda

```python
for size in [100, 300, 500]:

    plt.scatter(
        [],
        [],
        s=size,
        label=str(size)
    )

plt.legend()
```

## Crear múltiples leyendas

```python
from matplotlib.legend import Legend

leg = Legend(
    ax,
    lines,
    ['A', 'B'],
    loc='lower right'
)

ax.add_artist(leg)
```

---

# 23. CONCLUSIÓN GENERAL

Matplotlib proporciona herramientas muy flexibles para representar y analizar datos mediante gráficos de líneas y gráficos de dispersión.

Los gráficos de líneas permiten visualizar funciones y tendencias, personalizando el color, el estilo y los límites de los ejes.

Los gráficos de dispersión permiten representar observaciones individuales y utilizar características visuales como el tamaño, el color y la transparencia para incorporar dimensiones adicionales de información.

La diferencia entre `plt.plot()` y `plt.scatter()` es especialmente importante: aunque ambas funciones pueden representar puntos, `plt.scatter()` ofrece una mayor capacidad de personalización individual, mientras que `plt.plot()` puede ser más eficiente con grandes conjuntos de datos.

Por otra parte, las leyendas permiten interpretar correctamente los elementos visuales de una representación. Matplotlib ofrece herramientas para personalizar su posición, apariencia y contenido, así como mecanismos más avanzados para construir leyendas personalizadas y múltiples.

**Los conceptos fundamentales de este tema son:**

1. Comprender la diferencia entre `Figure` y `Axes`.
2. Saber crear gráficos mediante `plt.plot()` y `ax.plot()`.
3. Personalizar los colores y estilos de las líneas.
4. Controlar los límites y las proporciones de los ejes.
5. Añadir títulos y etiquetas.
6. Crear y personalizar leyendas.
7. Crear gráficos de dispersión mediante `plt.scatter()`.
8. Representar varias dimensiones mediante la posición, el tamaño y el color de los puntos.
9. Comprender las diferencias de rendimiento entre `plot()` y `scatter()`.
10. Crear leyendas personalizadas y múltiples mediante objetos `Legend`.

Dominar estos conceptos proporciona una base sólida para realizar visualizaciones de datos más completas, informativas y personalizadas utilizando Matplotlib.




<hr>








# Histogramas, Binnings y Densidades en Python con Matplotlib y NumPy

Un simple histograma puede ser un gran primer paso para comprender las características esenciales de un conjunto de datos. Permite visualizar la distribución de los valores, identificar la tendencia central, observar la dispersión y detectar la presencia de sesgos o valores atípicos (outliers).

---

## 1. Histogramas Unidimensionales

La forma más directa de trazar un histograma en una dimensión es utilizando la función `plt.hist()` de Matplotlib.

### Configuración Inicial y Datos de Ejemplo
Para ilustrar los conceptos, se genera un conjunto de datos con una distribución normal (gaussiana) utilizando NumPy:

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt

# Configuración del estilo de gráficos
plt.style.use('seaborn-v0_8')

# Generación de 1000 números aleatorios con distribución normal estándar
data = np.random.randn(1000)
```

### Gráfico Básico
El comando más simple divide los datos automáticamente en casillas o intervalos (*bins*):

```python
plt.hist(data, bins=100);
```

### Personalización del Histograma
La función `plt.hist()` ofrece múltiples opciones para ajustar tanto el cálculo matemático de los intervalos como la visualización estética:

*   **`bins`**: Especifica el número de intervalos o casillas en los que se dividirá el rango de datos.
*   **`alpha`**: Ajusta el grado de transparencia de las barras (valor entre `0` y `1`). Es una propiedad sumamente útil al superponer múltiples distribuciones en un mismo gráfico para evitar que se oculten entre sí.
*   **`color`**: Cambia el color de relleno de las barras (ej. `'steelblue'`).

```python
plt.hist(data, bins=30, alpha=0.5, color='steelblue');
```

### Comparación de Varias Distribuciones
Combinando el parámetro `alpha` con diferentes configuraciones de diccionarios (`kwargs`), se pueden contrastar múltiples conjuntos de datos de manera limpia:

```python
x1 = np.random.normal(0, 0.8, 1000)
x2 = np.random.normal(-2, 1, 1000)
x3 = np.random.normal(3, 2, 1000)

kwargs = dict(alpha=0.5, bins=50)

plt.hist(x1, **kwargs, label="X1")
plt.hist(x2, **kwargs, label="X2")
plt.hist(x3, **kwargs, label="X3")
plt.legend();
```

### Cálculo Numérico sin Gráfico (`np.histogram`)
Si solo se requiere realizar el cálculo matemático del histograma (contar cuántos puntos caen dentro de cada intervalo) sin generar una representación visual, NumPy proporciona la función `np.histogram()`:

```python
counts, bin_edges = np.histogram(x1, bins=50)
print(counts) # Devuelve un array con las frecuencias
print(bin_edges) # Devuelve los límites de cada intervalo (bin)
```

---

## 2. Histogramas Bidimensionales y Binnings

De la misma manera que se crean histogramas en una dimensión dividiendo una línea numérica en intervalos, se pueden construir histogramas en dos dimensiones dividiendo los puntos de un plano cartesiano en casillas bidimensionales.

### Datos de Ejemplo (Distribución Gaussiana Multivariante)
Se define una matriz de coordenadas `x` e `y` extraída de una distribución normal bidimensional correlacionada:

```python
mean = [0, 0]
cov = [[1, 1], [1, 2]]
x, y = np.random.multivariate_normal(mean, cov, 10000).T
```

### A. Casillas Cuadradas: `plt.hist2d`
Una forma directa de estructurar esta información es con casillas cuadradas usando la función `plt.hist2d()`:

```python
plt.hist2d(x, y, bins=100, cmap='Blues');
cb = plt.colorbar()
cb.set_label('counts in bin')
```
*   **`cmap`**: Aplica un mapa de colores (Colormap) para representar la densidad de frecuencias.
*   **`plt.colorbar()`**: Añade una barra lateral que funciona como leyenda matemática para mapear los colores con la cantidad de frecuencias detectadas.

Para realizar el cálculo puramente numérico en dos dimensiones (o más), NumPy ofrece las funciones homólogas:
*   `np.histogram2d(x, y, bins=10)`
*   `np.histogramdd` (Para generalizaciones en más de dos dimensiones).

### B. Casillas Hexagonales: `plt.hexbin`
El binning cuadrado puede generar artefactos visuales debido a las orientaciones de los ejes. Una alternativa natural y estéticamente eficiente es usar hexágonos regulares. Matplotlib lo resuelve mediante la rutina `plt.hexbin()`:

```python
plt.hexbin(x, y, gridsize=10, cmap='Blues')
cb = plt.colorbar(label='count in bin')
```
*   **`gridsize`**: Controla el tamaño y cantidad de la estructura de hexágonos en el gráfico.
*   **Propiedades Avanzadas**: Admite el paso de un argumento para ponderar (`weights`) cada punto y cambiar el tipo de acumulación de datos en cada hexágono mediante cualquier agregado de NumPy (como obtener la media o la desviación estándar en lugar de la suma de frecuencias).

---

## 3. Personalización de Barras de Colores (Colorbars)

Las barras de colores (`colorbar`) funcionan como leyendas continuas que asocian tonalidades con rangos de valores cuantitativos. En Matplotlib, una barra de colores es una instancia independiente de un eje (`plt.Axes`).

### Categorías de Mapas de Colores (Colormaps)
Elegir el mapa de colores adecuado es crítico para no sesgar la interpretación de los datos. Se clasifican principalmente en tres familias:

1.  **Secuenciales**: Formados por una secuencia continua y monótona de colores y brillo (ej. `binary` o `viridis`). Son ideales para datos cuantitativos incrementales.
2.  **Divergentes**: Contienen dos colores distintos que convergen en un centro neutro (ej. `RdBu` o `PuOr`). Ideales para resaltar desviaciones positivas y negativas respecto a una media o valor central.
3.  **Cualitativos o Cíclicos**: Mezclan colores sin una secuencia de brillo lineal (ej. `rainbow` o `jet`). Son útiles para datos categóricos, pero **pésimos para representar datos cuantitativos continuos**.

### El Problema de los Mapas Cualitativos (Ejemplo: `jet`)
El mapa de colores `jet` (antiguo esquema por defecto en Matplotlib) rompe la progresión uniforme del brillo. Al convertir un mapa de color `jet` a escala de grises, se observan franjas brillantes falsas en zonas intermedias, lo que introduce un sesgo visual inconsciente en el ojo humano, haciendo que resalten regiones sin justificación matemática.

Mapas modernos como **`viridis`** o **`cubehelix`** garantizan una progresión perfectamente lineal de la luminosidad, permitiendo una correcta interpretación de los datos e incluso una correcta visualización si el gráfico se imprime en blanco y negro.

```python
# Aplicación de un colormap secuencial correcto
plt.imshow(I, cmap='viridis')
plt.colorbar();
```

### Límites de Color y Extensiones (`extend`)
Cuando los datos contienen ruido o valores extremos, los límites por defecto del mapa de colores pueden verse afectados, ocultando los patrones principales. Esto se soluciona limitando el rango visual (`plt.clim`) y extendiendo los extremos en forma de flechas indicativas mediante el parámetro `extend`:

```python
# Fijación manual de límites de color ignorando extremos ruidosos
plt.imshow(I, cmap='RdBu')
plt.colorbar(extend='both')
plt.clim(-1, 1);  # Fija los límites de color entre -1 y 1
```

### Mapas de Colores Discretos
Si en lugar de una transición de color continua se desea una visualización por pasos o intervalos discretos, se puede recurrir a la función `plt.cm.get_cmap()` pasando el número de divisiones deseadas:

```python
# Divide el mapa de colores en 6 bloques discretos bien definidos
plt.imshow(I, cmap=plt.cm.get_cmap('Blues', 6))
plt.colorbar()
plt.clim(-1, 1);
```




<hr>








# Análisis Exploratorio de Datos (EDA) con Seaborn

El objetivo principal del análisis visual de datos no consiste únicamente en saber programar gráficos en Python, sino en **comprender qué tipo de gráfica utilizar en cada momento**. Antes de representar los datos, es indispensable dar un paso atrás para identificar su naturaleza y cuántas variables intervienen en el análisis.

---

## 1. Clasificación Inicial del Análisis y Tipos de Variables

Antes de representar cualquier dato, es imprescindible comprender qué tipo de variable tenemos y cuántas vamos a cruzar:
* **Una variable numérica** (cuantitativa).
* **Una variable categórica** (cualitativa).
* **Dos variables numéricas**.
* **Tres o más variables numéricas**.
* **Dos variables categóricas**.
* **Combinación de variables numéricas y categóricas**.

> **Nota teórica:** Teniendo clara esta clasificación y apoyándose en un buen catálogo de gráficas (como [data-to-viz.com](https://data-to-viz.com)), la elección de la visualización resulta mucho más sencilla.

---

## 2. Análisis Univariante

Este análisis se centra en estudiar el comportamiento de una única variable de forma aislada.

### 2.1. Variables Cuantitativas (Numéricas)
Se utilizan para observar cómo se distribuyen los datos, dónde se concentran más, cuál es su dispersión, si presentan asimetría y si existen valores atípicos (*outliers*).

* **Diagrama de Densidad (KDE - Kernel Density Estimation):**
  * **Función:** Permite visualizar la distribución continua de los datos y su probabilidad de aparición.
  * **Implementación:** Se utiliza `sns.distplot()` (actualmente reemplazada por `sns.histplot(..., kde=True)` o `sns.displot()`).
* **Histograma:**
  * **Función:** Muestra la frecuencia de aparición de todos los valores agrupados en intervalos (*bins*).
  * **Diferencia clave con la densidad:** Es muy similar al diagrama de densidad, pero en el histograma el eje Y representa un conteo absoluto de observaciones en lugar de la probabilidad de aparición.
  * **Utilidad adicional:** Permite agrupar visualmente una variable numérica continua para sugerir una posible categorización.
* **Gráfico de Alfombra (*Rug plot*):**
  * **Función:** Mediante el argumento `rug=True`, dibuja pequeñas marcas verticales sobre el eje X por cada dato individual, ofreciendo una forma muy visual de observar la concentración exacta de los valores.
* **Diagrama de Caja (*Boxplot*):**
  * **Función:** Resume la distribución a través de sus percentiles y cuartiles: mínimo (percentil 0 / Q0), primer cuartil (percentil 25 / Q1), mediana (percentil 50 / Q2), tercer cuartil (percentil 75 / Q3) y máximo (percentil 100 / Q4).
  * **Ventaja principal:** Da una información muy parecida a los gráficos anteriores, pero destaca mucho más la presencia de **outliers** (valores atípicos). Se genera con `sns.boxplot()`.
* **Diagrama de Violín (*Violinplot*):**
  * **Función:** Es equivalente a un diagrama de caja, pero sustituye la caja rectangular por la curva de la función de distribución de densidad.
  * **Implementación:** Se genera con `sns.violinplot()` y permite añadir detalles internos como `inner="stick"` para visualizar cada observación.

### 2.2. Variables Cualitativas (Categóricas)
Para representar una variable categórica, el enfoque teórico consiste en observar su **frecuencia de valores** (cuántas veces aparece cada categoría).

* **Gráfico de Conteo (*Countplot*):**
  * **Función:** Es el equivalente al histograma para variables categóricas; representa mediante barras la frecuencia absoluta de cada categoría (`sns.countplot()`).
* **Gráfico de Piruleta (*Lollipop chart*):**
  * **Función:** Alternativa visual más limpia al gráfico de barras tradicional para mostrar conteos ordenados. Se construye combinando líneas horizontales (`plt.hlines`) con puntos en sus extremos (`plt.plot(..., "o")`).
* **Gráfico de Tarta y de Donut (*Pie chart / Donut chart*):**
  * **Función:** Representan la proporción porcentual (`autopct`) de cada categoría respecto al total.
  * **Construcción del Donut:** Se crea a partir de un `plt.pie()` tradicional al que se le superpone un círculo blanco en el centro mediante `plt.Circle((0,0), ...)`.

---

## 3. Análisis Bivariante y Multivariante

Este enfoque permite comparar variables entre sí para descubrir relaciones, diferencias entre grupos o correlaciones.

### 3.1. Comparativa de Variables Cuantitativas (2 a 4 variables)
* **Boxplots múltiples + Swarmplot:**
  * **Función:** Permiten comparar qué tan diferentes son las distribuciones de varias variables numéricas lado a lado.
  * **Mejora visual:** Un *boxplot* por sí solo oculta la distribución exacta de los puntos internos. Superponer un `sns.swarmplot()` encima del `sns.boxplot()` evita que se escape información al mostrar cada observación individual sin solapamiento.
* **Diagramas de Densidad e Histogramas Superpuestos:**
  * **Función:** Permiten contrastar la forma y el solapamiento de las distribuciones de distintas variables numéricas en un mismo gráfico (`sns.kdeplot(..., shade=True)`) o en una cuadrícula de subgráficos (`plt.subplots`).
* **Gráfico de Dispersión (*Scatter plot*):**
  * **Función:** Representa la relación entre dos variables numéricas en los ejes X e Y (`sns.scatterplot()`).
  * **Clasificación visual:** Al añadir una variable categórica mediante el parámetro `hue` (color), permite observar claramente si la combinación de esas dos variables numéricas sirve para distinguir o separar grupos.
* **Jointplot:**
  * **Función:** Gráfica compuesta (`sns.jointplot()`) que muestra en el panel central la relación bivariante entre dos variables numéricas y en los márgenes superior y derecho sus respectivas distribuciones univariantes.
  * **Variantes:** Además de puntos tradicionales, admite representaciones hexagonales (`kind="hex"`) o de densidad (`kind="kde"`) para evitar la saturación cuando hay muchos datos.

### 3.2. Comparativa de Múltiples Variables Numéricas
* **Mapa de Calor (*Heatmap*):**
  * **Función:** Es la herramienta perfecta para representar visualmente una **matriz de correlación** (`.corr()`) entre múltiples variables numéricas (`sns.heatmap()`).
  * **Buenas prácticas teóricas:** Es crucial utilizar una buena paleta de colores divergente (evitando escalas que dificulten la lectura) y fijar los límites de la escala entre -1 y 1 (`vmin=-1, vmax=1`) para interpretar fielmente las correlaciones inversas y directas.
  * **Uso alternativo (1 numérica vs. 2 categóricas):** También permite cruzar una variable numérica frente a dos variables categóricas agrupadas previamente. Se recomienda que ambas variables categóricas tengan pocos valores únicos para que el gráfico sea legible.
* **Correlograma (*Pairplot*):**
  * **Función:** Genera una matriz de gráficos (`sns.pairplot()`) que cruza todas las variables numéricas de un dataset entre sí. Muestra gráficos de dispersión para cada par de variables y la distribución individual en la diagonal principal, permitiendo detectar correlaciones lineales de un vistazo.
  * **Recomendación práctica:** **No** debe realizarse con demasiadas variables a la vez porque el gráfico pierde legibilidad; en datasets grandes se recomienda hacerlo por partes.





<hr>








# Visualización de Datos con Plotly en Python

El uso de la librería **Plotly** (y herramientas complementarias como `WordCloud`) para crear gráficos interactivos y con calidad de publicación en Python, basado en el análisis del conjunto de datos de rankings universitarios (`timesData.csv`).

---

## 1. Introducción a Plotly

La librería gráfica **Plotly** para Python permite crear visualizaciones interactivas en línea con calidad de publicación. A diferencia de otras librerías estáticas, las figuras generadas permiten al usuario interactuar directamente en el navegador: pasar el cursor sobre los puntos para ver detalles, hacer zoom, desplazarse por los ejes y mostrar u ocultar series de datos haciendo clic en la leyenda.

Entre los tipos de gráficos que se pueden construir se incluyen:
* Gráficos de líneas (*Line plots*) y de dispersión (*Scatter plots*).
* Gráficos de área (*Area charts*) y de barras (*Bar charts*).
* Gráficos circulares (*Pie charts*) y de burbujas (*Bubble charts*).
* Histogramas (*Histograms*) y diagramas de caja (*Box plots*).
* Matrices de dispersión (*Scatter plot matrix*) y mapas de calor (*Heatmaps*).
* Gráficos insertados (*Inset plots*), subgráficos múltiples (*Multiple subplots*) y gráficos en 3D.

### Estructura Básica de un Gráfico en Plotly
Para construir la mayoría de las visualizaciones utilizando el módulo `plotly.graph_objs` (importado comúnmente como `go`), se sigue una estructura estándar compuesta por los siguientes elementos:

1. **Trazos (`traces`)**: Son los objetos que definen cada serie de datos a graficar (por ejemplo, `go.Scatter`, `go.Bar`, `go.Pie`, etc.). Contienen las coordenadas, el modo de visualización, colores y textos emergentes.
2. **Datos (`data`)**: Es una lista de Python (`[trace1, trace2, ...]`) donde se agrupan todos los trazos que formarán parte de la misma figura.
3. **Diseño (`layout`)**: Es un diccionario o un objeto `go.Layout` que controla la apariencia general del gráfico: título principal, configuración de los ejes (`xaxis`, `yaxis`), modo de agrupación, anotaciones, entre otros.
4. **Figura (`fig`)**: Es el contenedor final (`go.Figure(data=data, layout=layout)`) que une los datos con el diseño.
5. **Renderizado (`iplot()` / `fig.show()`)**: Función encargada de dibujar la figura interactiva en el entorno de trabajo (como Jupyter Notebook o Google Colab).

---

## 2. Carga de Datos y Explicación de Variables

El análisis se desarrolla utilizando el archivo `timesData.csv`, el cual contiene **2,603 registros** y **14 características (columnas)** relacionadas con el ranking mundial de universidades entre los años 2011 y 2016:

* **`world_rank`**: Posición de la universidad en el ranking mundial.
* **`university_name`**: Nombre de la institución educativa.
* **`country`**: País al que pertenece la universidad.
* **`teaching`**: Puntuación obtenida en enseñanza (ambiente de aprendizaje).
* **`international`**: Puntuación en perspectiva internacional (personal, estudiantes e investigación).
* **`research`**: Puntuación en investigación (volumen, ingresos y reputación).
* **`citations`**: Puntuación en citas (influencia de la investigación).
* **`income`**: Puntuación en ingresos de la industria (transferencia de conocimiento).
* **`total_score`**: Puntuación global total.
* **`num_students`**: Número total de estudiantes.
* **`student_staff_ratio`**: Proporción de estudiantes por cada miembro del personal académico.
* **`international_students`**: Porcentaje de estudiantes internacionales.
* **`female_male_ratio`**: Proporción entre estudiantes mujeres y hombres.
* **`year`**: Año de evaluación del ranking.

---

## 3. Tipos de Gráficos y su Teoría

### 3.1. Gráficos de Líneas (*Line Charts*)
Se utilizan para visualizar tendencias o comparar métricas a lo largo de una secuencia ordenada (por ejemplo, comparar las citas y la enseñanza frente al ranking mundial de las 100 mejores universidades).

* **Parámetros clave en `go.Scatter`**:
  * `x`: Datos del eje horizontal.
  * `y`: Datos del eje vertical.
  * `mode`: Define el estilo del trazo. Puede ser `'lines'` (solo líneas), `'markers'` (solo puntos) o `'lines+markers'` (líneas con puntos marcados).
  * `name`: Nombre de la serie que aparecerá en la leyenda.
  * `marker`: Diccionario para personalizar los puntos/líneas, como `color` en formato `rgba(rojo, verde, azul, opacidad)`.
  * `text`: Información adicional que se muestra al pasar el cursor (*hover*) sobre cada punto.
* **Parámetros clave en `layout`**:
  * `title`: Título principal del gráfico.
  * `xaxis`: Diccionario con propiedades del eje X, como `title` (etiqueta del eje) y `ticklen` (longitud de las marcas de graduación).

---

### 3.2. Gráficos de Dispersión (*Scatter Charts*)
Permiten observar la distribución y relación entre dos variables numéricas mediante puntos individuales (por ejemplo, citas frente al ranking mundial en los años 2014, 2015 y 2016).

* **Configuración específica**:
  * Utiliza `go.Scatter` con `mode = "markers"`.
  * En `layout`, dentro de los diccionarios `xaxis` y `yaxis`, se puede configurar `zeroline = False` para ocultar la línea base del cero y limpiar visualmente el gráfico.

---

### 3.3. Gráficos de Barras (*Bar Charts*)
Ideales para comparar cantidades discretas entre diferentes categorías (por ejemplo, comparar las puntuaciones de citas y enseñanza de las 3 mejores universidades en 2014).

* **Sintaxis y parámetros en `go.Bar`**:
  * Se pueden definir usando la clase `go.Bar(...)` o directamente mediante diccionarios de Python especificando `'type': 'bar'`.
  * `x` e `y`: Categorías y valores respectivamente.
  * `marker`: Permite definir el color de relleno (`color`) y el borde de cada barra mediante un subdiccionario `line = dict(color=..., width=...)`.
* **Modos de visualización en `layout` (`barmode`)**:
  * `'group'`: Coloca las barras de diferentes trazos una al lado de la otra para cada categoría.
  * `'relative'` (o apilado): Apila las barras una encima de la otra para mostrar el acumulado.

---

### 3.4. Gráficos Circulares y de Dona (*Pie Charts*)
Se emplean para representar proporciones o porcentajes de un todo (por ejemplo, la proporción de estudiantes entre las 7 mejores universidades en 2016).

* **Parámetros principales**:
  * `values`: Lista de valores numéricos que determinan el tamaño de cada sector.
  * `labels`: Etiquetas correspondientes a cada sector.
  * `hoverinfo`: Define qué datos se muestran al pasar el cursor (ej. `'label+percent+name'`).
  * `hole`: Valor entre `0` y `1` que define el tamaño del agujero central; si es mayor a `0` (ej. `0.3`), transforma el gráfico circular en un **gráfico de dona**.
  * `domain`: Controla el área que ocupa el gráfico dentro del lienzo.
  * `annotations` (en `layout`): Lista de diccionarios para añadir textos personalizados en coordenadas específicas (`x`, `y`), con control de fuente (`font`) y flechas (`showarrow`).

---

### 3.5. Gráficos de Burbujas (*Bubble Charts*)
Es una extensión del gráfico de dispersión que permite visualizar **hasta cuatro dimensiones** de datos simultáneamente en un plano 2D:

1. **Primera dimensión (`x`)**: Posición en el eje horizontal.
2. **Segunda dimensión (`y`)**: Posición en el eje vertical.
3. **Tercera dimensión (`marker.color`)**: Representada mediante una escala de colores (ej. puntuación internacional). Se activa la barra de referencia con `'showscale': True`.
4. **Cuarta dimensión (`marker.size`)**: Representada por el tamaño/diámetro de cada burbuja (ej. número de estudiantes).

---

### 3.6. Histogramas (*Histograms*)
Muestran la distribución de frecuencias de una variable numérica continua, permitiendo comparar cómo se distribuyen los datos en distintos periodos (ej. proporción estudiante-profesor en 2011, 2012 y 2013).

* **Parámetros clave**:
  * `go.Histogram`: Solo requiere definir el eje `x` con los datos a agrupar.
  * `opacity`: Controla la transparencia de las barras (ej. `0.9`), fundamental cuando se superponen múltiples histogramas.
  * `barmode` (en `layout`): Puede ser `'overlay'` (superpuesto, para ver dónde coinciden las distribuciones) o `'stack'` (apilado).

---

### 3.7. Nube de Palabras (*Word Cloud*)
Aunque no pertenece nativamente a Plotly (se implementa con las librerías `wordcloud` y `matplotlib`), es una herramienta visual muy útil para analizar frecuencias de texto (ej. identificar qué países aparecen con mayor frecuencia en el ranking de 2011).

* **Funcionamiento**:
  * `WordCloud(background_color='white', width=..., height=...)`: Configura el lienzo de la nube.
  * `.generate(" ".join(lista_textos))`: Procesa una cadena de texto unificada y asigna un tamaño de fuente proporcional a la frecuencia de aparición de cada palabra.

---



### 3.8. Diagramas de Caja (*Box Plots*)
Los diagramas de caja son una herramienta estadística esencial para visualizar la distribución, dispersión, simetría y detección de valores atípicos de un conjunto de datos numéricos (por ejemplo, comparar la puntuación total y la puntuación de investigación de las universidades en el año 2015).

* **Conceptos estadísticos fundamentales representados**:
  * **Mediana (Percentil 50)**: Es el valor central del conjunto de datos una vez ordenado. Divide la muestra en dos mitades exactas, indicando que el 50% de los datos son menores o iguales a este valor.
  * **Primer Cuartil (Q₁ - Percentil 25)**: Conocido como cuartil inferior, marca el punto donde el 25% de los datos se encuentran por debajo de este valor.
  * **Tercer Cuartil (Q₃ - Percentil 75)**: Conocido como cuartil superior, indica que el 75% de los datos se encuentran por debajo de este valor.
  * **Rango Intercuartílico (IQR)**: Representa la altura de la caja central y mide la dispersión del 50% central de los datos. Se calcula mediante la fórmula:
    \[IQR = Q_3 - Q_1\]

  * **Bigotes (*Whiskers*)**: Son las líneas que se extienden desde los bordes de la caja (Q₁ y Q₃) hasta una distancia máxima de 1.5 × IQR para delimitar el rango normal de los datos.
  * **Valores Atípicos (*Outliers*)**: Son observaciones individuales que caen más allá de los límites establecidos por los bigotes (es decir, a una distancia superior a 1.5 × IQR).
* **Parámetros clave en `go.Box`**:
  * `y`: Serie de datos numéricos que se desea analizar.
  * `name`: Etiqueta identificativa de la caja en el eje y la leyenda.
  * `marker`: Diccionario para personalizar el color de la caja y sus puntos atípicos.

---

### 3.9. Matriz de Dispersión (*Scatter Matrix Plots*)
Una matriz de dispersión permite analizar simultáneamente la covarianza y las relaciones de correlación entre **más de dos variables** numéricas (por ejemplo, evaluar la relación conjunta entre `research`, `international` y `total_score` en 2015).

* **Preprocesamiento previo**: Antes de generar la matriz, es necesario limpiar valores no numéricos (como reemplazar guiones `'-'` por `'0'`) y convertir las columnas al tipo flotante (`float`).
* **Implementación mediante `plotly.figure_factory` (`ff`)**:
  * Función principal: `ff.create_scatterplotmatrix(dataframe, ...)`.
  * `diag`: Define el tipo de gráfico que se mostrará en la diagonal principal de la matriz para cada variable individual (por ejemplo, `'box'` para diagramas de caja, histogramas o curvas de densidad).
  * `index`: Columna de referencia (como un índice de ranking) utilizada para mapear el degradado de color de los puntos.
  * `colormap`: Define la paleta o mapa de colores aplicado a los datos (por ejemplo, `'Portland'`).
  * `colormap_type`: Especifica cómo se interpreta el mapa de colores (categórica o continua).
  * `height` y `width`: Definen el alto y ancho total de la matriz en píxeles (ej. `700` x `700`).

---

### 3.10. Gráficos Insertados (*Inset Plots*)
Un gráfico insertado consiste en colocar dos gráficos dentro de un mismo marco: un gráfico principal que ocupa todo el lienzo y un gráfico secundario más pequeño incrustado en una zona específica (por ejemplo, visualizar la puntuación de enseñanza frente al ranking mundial como gráfico principal, e insertar los ingresos frente al ranking en la esquina superior derecha).

* **Configuración de ejes y dominios**:
  * El primer trazo (`trace1`) utiliza por defecto los ejes principales (`x` e `y`).
  * Al segundo trazo (`trace2`) se le asignan ejes secundarios explícitos: `xaxis='x2'` y `yaxis='y2'`.
  * En `go.Layout`, se configuran `xaxis2` y `yaxis2` utilizando la propiedad `domain` (una lista `[inicio, fin]` con proporciones entre `0` y `1`, como `[0.6, 0.95]`) y `anchor` (`anchor='y2'`, `anchor='x2'`) para delimitar el recuadro exacto donde aparecerá el gráfico insertado.

---

### 3.11. Gráficos de Dispersión 3D con Escala de Color (*3D Scatter Plot with Colorscaling*)
Cuando dos dimensiones no bastan para comprender la estructura o patrones ocultos de un conjunto de datos, añadir una tercera dimensión espacial mejora significativamente la inteligibilidad. Además, al incorporar una escala de color, es posible representar **hasta cuatro dimensiones** en una sola visualización interactiva.

* **Parámetros clave en `go.Scatter3d`**:
  * `x`, `y`, `z`: Definen las tres coordenadas espaciales de cada punto (por ejemplo, `world_rank`, `research` y `citations`).
  * `mode`: Se establece en `'markers'` para representar cada registro como un punto en el espacio tridimensional.
  * `marker`: Diccionario donde se configura el tamaño del punto (`size`), el color (`color`) y la escala de colores (`colorscale`), que actúa como la cuarta dimensión visual.

---

### 3.12. Subgráficos Múltiples (*Multiple Subplots*)
Los subgráficos múltiples permiten dividir el área de dibujo en varias secciones independientes para comparar diferentes variables de forma paralela dentro de una misma figura (por ejemplo, comparar `research`, `citations`, `income` y `total_score` frente al `world_rank` en una cuadrícula de 2 × 2).

* **Configuración de cuadrícula mediante dominios**:
  * Cada trazo (`trace1`, `trace2`, `trace3`, `trace4`) se vincula a su propio par de ejes (`x1`/`y1`, `x2`/`y2`, `x3`/`y3`, `x4`/`y4`).
  * En `go.Layout`, se define el espacio de cada cuadrante mediante `domain`:
    * **Columna izquierda (`xaxis`, `xaxis3`)**: `domain=[0, 0.45]` (ocupa del 0% al 45% del ancho).
    * **Columna derecha (`xaxis2`, `xaxis4`)**: `domain=[0.55, 1]` (ocupa del 55% al 100% del ancho, dejando un 10% de separación central).
    * **Fila inferior (`yaxis`, `yaxis2`)**: `domain=[0, 0.45]` (ocupa del 0% al 45% de la altura).
    * **Fila superior (`yaxis3`, `yaxis4`)**: `domain=[0.55, 1]` (ocupa del 55% al 100% de la altura).
  * Cada eje se enlaza con su perpendicular mediante la propiedad `anchor` (ej. `anchor='y1'`, `anchor='x1'`).

---

### 3.13. Mapas Geográficos (*Scatter Geo* con `Plotly Express`)
Como complemento a `graph_objs`, se introduce `plotly.express` (`px`), una interfaz de alto nivel que permite construir gráficos complejos de manera más concisa.

* **Implementación con `px.scatter_geo`**:
  * Permite proyectar datos sobre un mapa mundial utilizando códigos de país estándar.
  * `locations`: Columna con los códigos ISO de tres letras de cada país (`iso_alpha`).
  * `color`: Variable categórica que agrupa y colorea los puntos (ej. `continent`).
  * `hover_name`: Columna que muestra el nombre principal al pasar el cursor (ej. `country`).
  * `size`: Variable numérica que ajusta proporcionalmente el área de cada marcador en el mapa (ej. población `pop`).
  * `projection`: Tipo de proyección cartográfica utilizada para dibujar el globo (ej. `"natural earth"`).

---

## 4. Exportación de Gráficos a HTML

Las figuras generadas con Plotly mantienen toda su interactividad cuando se visualizan en un navegador web: permiten inspeccionar valores al pasar el cursor (*hover*), hacer zoom, desplazarse por los ejes (*pan*) y activar o desactivar trazos haciendo clic o doble clic en la leyenda.

* **Opciones de exportación**:
  * **Formatos estáticos**: Es posible guardar los gráficos como imágenes tradicionales en formato `PNG`, `JPEG`, `SVG` o `PDF`.
  * **Formato interactivo (`HTML`)**: Exportar la figura a un archivo `.html` independiente permite compartirla y abrirla en cualquier navegador web conservando todas sus funciones interactivas sin necesidad de ejecutar código Python.
* **Sintaxis de exportación**:
  ```python
  # Exporta el último objeto figura (fig) ejecutado a un archivo HTML interactivo
  fig.write_html("4 charts in one.html")
  ```








<hr>













# Python Interactive Maps with Folium

# 1. Introducción a Folium

## ¿Qué es Folium?

**Folium** es una librería de Python que permite crear mapas interactivos mediante la integración de datos geográficos con mapas basados en Leaflet.js.

Su principal utilidad es representar información geográfica de manera visual e interactiva, permitiendo añadir diferentes elementos a los mapas, como:

- Marcadores de ubicaciones.
- Círculos y áreas geográficas.
- Rutas entre diferentes puntos.
- Capas geográficas GeoJSON.
- Mapas coropléticos (Choropleth Maps).
- Mapas de calor (Heat Maps).
- Controles de navegación y medición.
- Imágenes superpuestas sobre mapas.
- Herramientas para dibujar elementos geográficos.

Folium es similar a `ipyleaflet`, aunque ambas librerías presentan diferencias en funcionalidad y sintaxis.

La principal ventaja de Folium es que permite generar mapas interactivos directamente desde Python y exportarlos como archivos HTML independientes.

## Instalación

Para instalar Folium:

```bash
pip install folium
```

También se pueden instalar las librerías auxiliares utilizadas en el notebook:

```bash
pip install geocoder
pip install numpy
pip install pandas
pip install vega_datasets
```

## Librerías utilizadas

```python
import folium
from folium import plugins
import geocoder
import numpy as np
import pandas as pd
from vega_datasets import data as vds
```

### Descripción de las librerías

| Librería | Utilidad |
|---|---|
| `folium` | Creación y personalización de mapas interactivos. |
| `folium.plugins` | Herramientas adicionales para ampliar las funcionalidades de los mapas. |
| `geocoder` | Obtención de coordenadas geográficas a partir de direcciones y nombres de lugares. |
| `numpy` | Generación y manipulación de datos numéricos y coordenadas. |
| `pandas` | Manipulación de datos tabulares mediante DataFrames. |
| `vega_datasets` | Acceso a conjuntos de datos de ejemplo, como información de aeropuertos. |

---

# 2. Creación de mapas básicos (Basic Maps)

La creación de un mapa es el primer paso para trabajar con Folium.

La función principal es:

```python
folium.Map()
```

Esta función permite inicializar un mapa interactivo.

Si no se especifican parámetros, Folium genera un mapa con sus valores predeterminados.

## Parámetros principales de folium.Map()

Los parámetros más importantes utilizados en el notebook son:

- `location`: coordenadas geográficas del centro del mapa.
- `zoom_start`: nivel de zoom inicial.
- `width`: anchura del mapa.
- `height`: altura del mapa.
- `control_scale`: permite mostrar una escala de distancias en el mapa.
- `tiles`: permite seleccionar el tipo de mapa o cartografía de fondo.

### Coordenadas geográficas

Las coordenadas se proporcionan mediante una lista con dos valores:

```python
location=[latitude, longitude]
```

Donde:

- `latitude`: latitud.
- `longitude`: longitud.

Es importante mantener este orden: primero latitud y después longitud.

### Ejemplo de creación de un mapa

```python
map1 = folium.Map(
    location=[43.2628099, -2.9369318],
    zoom_start=14,
    control_scale=True
)

map1
```

En este ejemplo:

- El mapa se centra en unas coordenadas geográficas concretas.
- `zoom_start=14` establece el nivel de ampliación inicial.
- `control_scale=True` muestra una escala de referencia.

Los parámetros `width` y `height` también pueden utilizarse para establecer las dimensiones del mapa.

```python
map1 = folium.Map(
    location=[43.2628099, -2.9369318],
    zoom_start=14,
    width=700,
    height=500
)
```

---

# 3. Guardar mapas (Save Map)

Folium permite exportar los mapas creados a archivos HTML.

Esto resulta especialmente útil porque permite visualizar los mapas fuera del entorno de Python, utilizando cualquier navegador web compatible.

Para guardar un mapa se utiliza el método:

```python
map.save('nombre_archivo.html')
```

### Ejemplo

```python
map1.save('map1.html')
```

El resultado es un archivo HTML que contiene el mapa interactivo.

**Ventajas de exportar a HTML:**

- Permite compartir mapas con otras personas.
- No requiere ejecutar nuevamente el código Python para visualizar el resultado.
- Facilita la integración de mapas en páginas web.
- Conserva las funcionalidades interactivas del mapa.

---

# 4. Tipos de mapas y capas cartográficas (Map Types)

Folium permite utilizar diferentes proveedores y estilos cartográficos para representar la información geográfica.

Estos estilos se conocen como *tiles* o capas cartográficas.

Cada tipo de mapa ofrece una representación visual diferente del territorio.

## Tipos de mapas utilizados

En el notebook aparecen los siguientes tipos:

| Tipo de mapa | Descripción |
|---|---|
| `OpenStreetMap` | Cartografía general con información de calles, ciudades y elementos geográficos. |
| `Stamen Terrain` | Representación del relieve y características físicas del terreno. |
| `Stamen Toner` | Estilo monocromático de alto contraste. |
| `Stamen Watercolor` | Representación cartográfica con apariencia de acuarela. |
| `CartoDB Positron` | Estilo claro y minimalista. |
| `CartoDB Dark_Matter` | Estilo oscuro, útil para determinadas visualizaciones. |

## Añadir diferentes capas al mapa

Para incorporar diferentes tipos de mapas se utiliza:

```python
folium.raster_layers.TileLayer()
```

### Ejemplo

```python
map_layer_control = folium.Map(
    location=[40.416719, -3.684016],
    zoom_start=12
)

folium.raster_layers.TileLayer(
    'Open Street Map'
).add_to(map_layer_control)

folium.raster_layers.TileLayer(
    'Stamen Terrain'
).add_to(map_layer_control)

folium.raster_layers.TileLayer(
    'Stamen Toner'
).add_to(map_layer_control)

folium.raster_layers.TileLayer(
    'Stamen Watercolor'
).add_to(map_layer_control)

folium.raster_layers.TileLayer(
    'CartoDB Positron'
).add_to(map_layer_control)

folium.raster_layers.TileLayer(
    'CartoDB Dark_Matter'
).add_to(map_layer_control)
```

## Control de capas (LayerControl)

Cuando un mapa contiene varias capas, es posible incorporar un control que permita al usuario activar o desactivar las diferentes representaciones cartográficas.

Para ello se utiliza:

```python
folium.LayerControl().add_to(map_layer_control)
```

El control permite cambiar entre los diferentes estilos de mapa sin necesidad de generar un mapa nuevo.

---

# 5. Herramientas adicionales: MiniMap y Fullscreen

Folium incorpora plugins que amplían las funcionalidades de los mapas.

Dos de ellos son `MiniMap` y `Fullscreen`.

## MiniMap

El plugin `MiniMap` permite incorporar un pequeño mapa de referencia dentro del mapa principal.

Su utilidad es facilitar la orientación espacial y proporcionar una visión general del área representada.

### Ejemplo

```python
map_with_mini = folium.Map(
    location=[40.416719, -3.684016],
    zoom_start=7
)

minimap = plugins.MiniMap(
    toggle_display=True
)

map_with_mini.add_child(minimap)
```

El parámetro:

- `toggle_display=True`: permite mostrar u ocultar el minimapa mediante un control.

## Fullscreen

El plugin `Fullscreen` permite visualizar el mapa ocupando toda la pantalla.

### Ejemplo

```python
plugins.Fullscreen(
    position='topright'
).add_to(map_with_mini)
```

El parámetro `position` permite establecer la ubicación del control.

En el ejemplo se coloca en la esquina superior derecha.

---

# 6. Marcadores geográficos (Markers)

Los marcadores permiten identificar ubicaciones concretas sobre un mapa.

Se utilizan para representar ciudades, edificios, aeropuertos, hospitales, puntos de interés o cualquier otra localización geográfica.

La clase principal es:

```python
folium.Marker()
```

## Parámetros principales

| Parámetro | Descripción |
|---|---|
| `location` | Coordenadas geográficas del marcador. |
| `popup` | Información que aparece al hacer clic sobre el marcador. |
| `tooltip` | Información que aparece al situar el cursor sobre el marcador. |
| `icon` | Permite personalizar el icono del marcador. |

### Ejemplo básico

```python
folium.Marker(
    location=[40.416719, -3.684016],
    popup='Madrid',
    tooltip='Haz clic'
).add_to(map1)
```

El marcador se incorpora al mapa mediante:

```python
.add_to(map1)
```

## 6.1. Obtener coordenadas mediante geocodificación (Geocoding)

La geocodificación consiste en transformar una dirección o un nombre de lugar en coordenadas geográficas.

En el notebook se utiliza la librería `geocoder` junto con OpenStreetMap.

La función utilizada es:

```python
geocoder.osm()
```

### Ejemplo

```python
import geocoder

place = 'Madrid, Hospital Ramon y Cajal'

address = geocoder.osm(place)

print(address)
```

El resultado contiene información geográfica del lugar buscado.

Entre los datos más importantes se encuentran:

- `address.lat`: latitud.
- `address.lng`: longitud.

Para obtener ambas coordenadas:

```python
address_latlng = [
    address.lat,
    address.lng
]
```

### Crear un marcador utilizando geocodificación

```python
place = 'Zaragoza'

address = geocoder.osm(place)

address_latlng = [
    address.lat,
    address.lng
]

map_madrid = folium.Map(
    location=[address.lat, address.lng],
    zoom_start=12
)

folium.Marker(
    address_latlng,
    popup=place,
    tooltip='click'
).add_to(map_madrid)

display(map_madrid)
```

**Concepto importante:** la geocodificación permite trabajar con direcciones y nombres de lugares sin tener que conocer previamente sus coordenadas geográficas.

---

# 7. Añadir múltiples marcadores utilizando DataFrames

Cuando se trabaja con numerosos puntos geográficos, no resulta práctico crear cada marcador individualmente.

Folium permite automatizar este proceso mediante estructuras de datos de Pandas.

En el notebook se utilizan dos procedimientos:

1. Recorrer un DataFrame mediante `iterrows()`.
2. Aplicar una función a todas las filas mediante `apply()`.

## 7.1. Obtener datos de aeropuertos

Se utiliza el conjunto de datos de aeropuertos disponible en `vega_datasets`.

```python
airports = vds.airports()

airports = airports[:25]

airports.head()
```

Este DataFrame contiene información de diferentes aeropuertos, incluyendo sus coordenadas geográficas y nombres.

Entre las columnas utilizadas destacan:

- `latitude`: latitud.
- `longitude`: longitud.
- `name`: nombre del aeropuerto.
- `city`: ciudad.

## 7.2. Utilizar iterrows()

El método `iterrows()` permite recorrer un DataFrame fila por fila.

Cada iteración proporciona el índice y los datos correspondientes a una fila.

### Ejemplo

```python
map_airports = folium.Map(
    location=[38, -98],
    zoom_start=4
)

for (index, row) in airports.iterrows():

    folium.Marker(
        location=[
            row.loc['latitude'],
            row.loc['longitude']
        ],
        popup=row.loc['name'] + ' ' + row['city'],
        tooltip='click'
    ).add_to(map_airports)

map_airports
```

En cada iteración:

1. Se obtiene una fila del DataFrame.
2. Se extraen la latitud y la longitud.
3. Se crea un marcador.
4. Se incorpora el nombre del aeropuerto y su ciudad al popup.
5. Se añade el marcador al mapa.

## 7.3. Utilizar apply()

Otra alternativa es emplear el método `apply()` de Pandas.

Este método permite aplicar una función a cada fila o columna de un DataFrame.

Cuando se utiliza:

```python
axis=1
```

La función se aplica fila por fila.

### Ejemplo

```python
map_airports2 = folium.Map(
    location=[38, -98],
    zoom_start=4
)

airports.apply(
    lambda row: folium.Marker(
        location=[
            row['latitude'],
            row['longitude']
        ],
        popup=row.loc['name'] + ' ' + row['city']
    ).add_to(map_airports2),
    axis=1
)

map_airports2
```

**Concepto importante:** tanto `iterrows()` como `apply()` permiten automatizar la creación de marcadores utilizando información almacenada en DataFrames.

---

# 8. Múltiples marcadores utilizando diccionarios

Otra forma de almacenar coordenadas geográficas es mediante diccionarios de Python.

En este caso, las claves representan los nombres de las ubicaciones y los valores contienen sus coordenadas.

### Ejemplo de diccionario

```python
markers_dict = {
    'Los Angeles': [34.041008, -118.246653],
    'Las Vegas': [36.169726, -115.143996],
    'Denver': [39.739448, -104.992450],
    'Chicago': [41.878765, -87.643267],
    'Manhattan': [40.782949, -73.969559]
}
```

Para recorrer el diccionario se puede utilizar:

```python
for elemento in markers_dict.items():
    print(elemento)
```

El método `items()` devuelve pares formados por:

- La clave: nombre de la ciudad.
- El valor: coordenadas geográficas.

## Crear múltiples marcadores desde un diccionario

```python
map_cities = folium.Map(
    location=[41, -99],
    zoom_start=4
)

for i in markers_dict.items():

    folium.Marker(
        location=i[1],
        popup=i[0]
    ).add_to(map_cities)

map_cities
```

En este ejemplo:

- `i[0]` contiene el nombre de la ciudad.
- `i[1]` contiene las coordenadas.

**Concepto importante:** los diccionarios permiten relacionar directamente cada ubicación con sus coordenadas, facilitando la creación de múltiples marcadores.

---

# 9. Marcadores personalizados (Custom Markers)

Folium permite modificar la apariencia de los marcadores mediante iconos personalizados.

Para ello se utiliza la clase:

```python
folium.Icon()
```

Se pueden personalizar aspectos como:

- El color del marcador.
- El icono que aparece en su interior.
- La biblioteca de iconos utilizada.

En el notebook se utilizan dos familias de iconos:

1. Font Awesome (`fa`).
2. Glyphicons (`glyphicon`).

## 9.1. Utilizar Font Awesome

Font Awesome proporciona una colección de iconos que pueden utilizarse para representar diferentes elementos.

Para especificar un icono de esta biblioteca se utiliza:

```python
folium.Icon(
    color='green',
    icon='bolt',
    prefix='fa'
)
```

### Ejemplo completo

```python
map_cm_fa = folium.Map(
    location=[38, -98],
    zoom_start=4
)

folium.Marker(
    location=[38, -98],
    popup='popup',
    icon=folium.Icon(
        color='green',
        icon='bolt',
        prefix='fa'
    )
).add_to(map_cm_fa)

map_cm_fa
```

## 9.2. Utilizar Glyphicons

Otra posibilidad es utilizar iconos de Bootstrap mediante Glyphicons.

En este caso se especifica:

```python
prefix='glyphicon'
```

### Ejemplo

```python
map_cm_glyphicon = folium.Map(
    location=[38, -98],
    zoom_start=4
)

folium.Marker(
    location=[38, -98],
    popup='popup',
    icon=folium.Icon(
        icon='glyphicon-plane',
        prefix='glyphicon'
    )
).add_to(map_cm_glyphicon)

map_cm_glyphicon
```

## 9.3. Múltiples marcadores personalizados desde un DataFrame

Es posible almacenar el nombre del icono correspondiente a cada ubicación dentro de un DataFrame.

### Crear el DataFrame

```python
cm_df = pd.DataFrame({
    'city': [
        'Los Angeles',
        'Las Vegas',
        'Denver',
        'Chicago',
        'Manhattan'
    ],
    'latitude': [
        34.041008,
        36.169726,
        39.739448,
        41.878765,
        40.782949
    ],
    'longitude': [
        -118.246653,
        -115.143996,
        -104.992450,
        -87.643267,
        -73.969559
    ],
    'icon': [
        'bicycle',
        'car',
        'bus',
        'truck',
        'motorcycle'
    ]
})
```

### Añadir los marcadores

Para recorrer el DataFrame se utiliza `itertuples()`.

Este método permite acceder a los valores de cada fila mediante atributos.

```python
map_cm_multiple = folium.Map(
    location=[38, -98],
    zoom_start=4
)

for i in cm_df.itertuples():

    folium.Marker(
        location=[
            i.latitude,
            i.longitude
        ],
        popup=i.city,
        icon=folium.Icon(
            icon=i.icon,
            prefix='fa'
        )
    ).add_to(map_cm_multiple)

map_cm_multiple
```

En este caso, cada ubicación tiene un icono diferente.

**Concepto importante:** los iconos personalizados permiten diferenciar visualmente categorías de ubicaciones y facilitan la interpretación del mapa.

## 9.4. Marcadores numerados con BeautifyIcon

Folium también permite crear marcadores numerados utilizando:

```python
plugins.BeautifyIcon()
```

Este plugin permite personalizar los marcadores mediante números y propiedades visuales.

Entre sus parámetros destacan:

- `number`: número que aparece en el marcador.
- `border_color`: color del borde.
- `border_width`: grosor del borde.
- `text_color`: color del texto.
- `inner_icon_style`: estilos CSS aplicados al icono interior.

### Ejemplo

```python
cm_enum_df = pd.DataFrame({
    'city': [
        'Los Angeles',
        'Las Vegas',
        'Denver',
        'Chicago',
        'Manhattan'
    ],
    'latitude': [
        34.041008,
        36.169726,
        39.739448,
        41.878765,
        40.782949
    ],
    'longitude': [
        -118.246653,
        -115.143996,
        -104.992450,
        -87.643267,
        -73.969559
    ],
    'icon_num': [1, 2, 3, 4, 5]
})
```

```python
map_enum_icons = folium.Map(
    [38, -98],
    zoom_start=4
)

for i in cm_enum_df.itertuples():

    folium.Marker(
        location=[
            i.latitude,
            i.longitude
        ],
        popup=i.city,
        icon=plugins.BeautifyIcon(
            number=i.icon_num,
            border_color='blue',
            border_width=1,
            text_color='red',
            inner_icon_style='margin-top:0px;'
        )
    ).add_to(map_enum_icons)

map_enum_icons
```

Este tipo de marcador resulta útil cuando se necesita identificar puntos mediante una numeración.

---

# 10. Marcadores circulares (Circle Markers)

Además de los marcadores convencionales, Folium permite representar ubicaciones mediante círculos.

Existen dos clases principales:

- `folium.Circle()`
- `folium.CircleMarker()`

Aunque visualmente pueden parecer similares, presentan una diferencia importante: la forma en la que se define su tamaño.

## 10.1. folium.Circle()

La clase `Circle` crea un círculo cuyo radio se especifica en metros.

### Parámetros

| Parámetro | Descripción |
|---|---|
| `location` | Coordenadas del centro del círculo. |
| `radius` | Radio del círculo en metros. |
| `color` | Color del borde. |

### Ejemplo

```python
folium.Circle(
    radius=100000,
    location=[38, -98],
    color='green'
).add_to(map_circle)
```

En este ejemplo, el círculo tiene un radio de 100.000 metros.

## 10.2. folium.CircleMarker()

La clase `CircleMarker` crea un círculo cuyo radio se especifica en píxeles.

### Parámetros

| Parámetro | Descripción |
|---|---|
| `location` | Coordenadas del centro. |
| `radius` | Radio en píxeles. |
| `color` | Color del borde. |
| `fill_color` | Color de relleno. |

### Ejemplo

```python
folium.CircleMarker(
    location=[39, -105],
    radius=25,
    color='blue',
    fill_color='yellow'
).add_to(map_circle)
```

## Diferencia entre Circle y CircleMarker

| Característica | Circle | CircleMarker |
|---|---|---|
| Tamaño | Metros | Píxeles |
| Referencia | Distancia geográfica | Tamaño visual |
| Uso | Representar áreas geográficas | Destacar puntos |

**Concepto importante:** el radio de `Circle` representa una distancia real sobre el territorio, mientras que el radio de `CircleMarker` representa un tamaño visual en pantalla.

---

# 11. Representación de rutas (Plot Route)

Folium permite representar recorridos entre diferentes ubicaciones mediante líneas que conectan una serie de coordenadas geográficas.

Para ello se utiliza:

```python
folium.PolyLine()
```

Esta clase permite dibujar una línea que conecta varios puntos siguiendo el orden de las coordenadas proporcionadas.

## Estructura de las coordenadas

Las coordenadas se almacenan en una lista de listas o en una lista de tuplas.

Cada elemento contiene:

```python
[latitude, longitude]
```

### Ejemplo de ruta

```python
route_lats_longs = [
    [34.041008, -118.246653],
    [36.169726, -115.143996],
    [39.739448, -104.992450],
    [41.878765, -87.643267],
    [40.782949, -73.969559]
]
```

## Dibujar la ruta con PolyLine

```python
map_plot_route = folium.Map(
    location=[38, -98],
    zoom_start=4
)

folium.PolyLine(
    route_lats_longs
).add_to(map_plot_route)

map_plot_route
```

La línea conecta los puntos en el orden en el que aparecen en la lista.

**Importante:** `PolyLine` representa una conexión visual entre coordenadas. No calcula automáticamente la ruta real por carreteras ni determina el recorrido óptimo.

## 11.1. Rutas animadas con AntPath

Otra posibilidad es utilizar:

```python
plugins.AntPath()
```

Este plugin permite representar rutas mediante una línea animada con un efecto de movimiento.

### Ejemplo

```python
map_ant_route = folium.Map(
    location=[38, -98],
    zoom_start=4
)

plugins.AntPath(
    route_lats_longs
).add_to(map_ant_route)

map_ant_route
```

La principal diferencia es visual:

- `PolyLine`: dibuja una línea convencional.
- `AntPath`: representa una línea animada.

---

# 12. Incorporación de capas GeoJSON (Overlay GeoJSON Layers)

GeoJSON es un formato basado en JSON que permite almacenar e intercambiar información geográfica.

Es especialmente útil para representar elementos geográficos como:

- Puntos.
- Líneas.
- Polígonos.
- Multipolígonos.
- Colecciones de diferentes elementos geográficos.

Folium permite incorporar archivos GeoJSON directamente a un mapa mediante:

```python
folium.GeoJson()
```

## Fuentes de archivos GeoJSON

En el notebook se mencionan diferentes formas de obtener estos archivos:

- Utilizar archivos GeoJSON existentes.
- Crear archivos personalizados mediante `geojson.io`.
- Utilizar el plugin `Draw` de Folium para dibujar elementos y exportarlos.
- Convertir archivos Shapefile a GeoJSON utilizando QGIS.

## Añadir un archivo GeoJSON al mapa

```python
map_geojson = folium.Map(
    location=[39.77, -86.15],
    zoom_start=7
)

folium.GeoJson(
    'data/indiana_outline_map.geojson',
    name='geojson indiana'
).add_to(map_geojson)

folium.LayerControl().add_to(map_geojson)

map_geojson
```

En este ejemplo:

1. Se crea un mapa centrado en Indiana.
2. Se carga un archivo GeoJSON.
3. Se añade la información geográfica al mapa.
4. Se incorpora un control de capas.

El parámetro `name` permite identificar la capa dentro del control.

**Concepto importante:** GeoJSON permite superponer información geográfica propia sobre un mapa base, facilitando la representación de límites territoriales y otras geometrías.

---

# 13. Subgrupos de capas GeoJSON (Subgroups with GeoJSON)

Cuando se trabaja con diferentes conjuntos de información geográfica, puede resultar interesante agruparlos en categorías.

Folium permite organizar capas mediante:

- `FeatureGroup`.
- `FeatureGroupSubGroup`.

## FeatureGroup

La clase `FeatureGroup` permite agrupar diferentes elementos geográficos dentro de una misma capa.

### Ejemplo

```python
all_subgroups = folium.FeatureGroup(
    name='all sales regions'
)

map_with_subgroups.add_child(all_subgroups)
```

En este caso se crea un grupo principal llamado `all sales regions`.

## FeatureGroupSubGroup

La clase `FeatureGroupSubGroup` permite crear subgrupos dentro de un grupo principal.

### Ejemplo completo

```python
map_with_subgroups = folium.Map(
    location=[39.77, -86.15],
    zoom_start=7
)

# Grupo principal
all_subgroups = folium.FeatureGroup(
    name='all sales regions'
)

map_with_subgroups.add_child(all_subgroups)

# Subgrupo 1
sales_region1 = plugins.FeatureGroupSubGroup(
    all_subgroups,
    'sales region 1'
)

map_with_subgroups.add_child(sales_region1)

# Subgrupo 2
sales_region2 = plugins.FeatureGroupSubGroup(
    all_subgroups,
    'sales region 2'
)

map_with_subgroups.add_child(sales_region2)

# Subgrupo 3
sales_region3 = plugins.FeatureGroupSubGroup(
    all_subgroups,
    'sales region 3'
)

map_with_subgroups.add_child(sales_region3)

# Incorporar archivos GeoJSON
folium.GeoJson(
    'data/sales_region1.geojson'
).add_to(sales_region1)

folium.GeoJson(
    'data/sales_region2.geojson'
).add_to(sales_region2)

folium.GeoJson(
    'data/sales_region3.geojson'
).add_to(sales_region3)

# Control de capas
folium.LayerControl(
    collapsed=False
).add_to(map_with_subgroups)

map_with_subgroups
```

## Utilidad de los subgrupos

Esta estructura permite organizar información geográfica jerárquicamente.

En el ejemplo se utiliza un grupo principal para las regiones comerciales y tres subgrupos correspondientes a diferentes regiones de ventas.

El parámetro:

```python
collapsed=False
```

hace que el control de capas aparezca inicialmente desplegado.

**Concepto importante:** `FeatureGroup` permite agrupar elementos y `FeatureGroupSubGroup` permite organizar esos elementos en subcategorías dentro de un grupo principal.

---

# 14. Mapas coropléticos (Choropleth Maps)

Un mapa coroplético es una representación cartográfica en la que diferentes regiones geográficas aparecen coloreadas según el valor de una variable estadística.

Se utiliza habitualmente para representar información agregada por territorios.

Algunos ejemplos de variables que pueden representarse son:

- Población.
- Densidad de población.
- Mortalidad.
- Nivel de ingresos.
- Porcentajes.
- Indicadores económicos.
- Datos demográficos.

La intensidad o el color de cada región permite identificar visualmente diferencias entre territorios.

## 14.1. Datos necesarios

Para construir un mapa coroplético se necesitan dos fuentes de información:

1. Un archivo GeoJSON con las geometrías de las regiones.
2. Un conjunto de datos con los valores estadísticos asociados a esas regiones.

En el notebook se utilizan:

- `geojson_indianacounties.geojson`: geometrías de los condados de Indiana.
- `indiana_population_by_county.csv`: población de cada condado.

## 14.2. Cargar el archivo GeoJSON

Los archivos GeoJSON pueden cargarse mediante la librería `json`.

```python
import json

with open(
    'data/geojson_indiana_counties.geojson'
) as f:

    geo_json_counties = json.load(f)
```

El contenido se almacena en un diccionario de Python.

Una estructura GeoJSON de tipo FeatureCollection contiene diferentes elementos dentro de la clave:

```python
geo_json_counties['features']
```

Cada elemento de `features` representa una entidad geográfica.

Dentro de cada entidad se encuentran:

- `geometry`: geometría del elemento.
- `properties`: propiedades o atributos asociados.
- `id`: identificador de la entidad, cuando está definido.

## 14.3. Crear identificadores para las regiones

Para relacionar las geometrías del archivo GeoJSON con los datos estadísticos es necesario disponer de un identificador común.

En el notebook se utiliza el nombre del condado:

```python
for i in geo_json_counties['features']:

    i['id'] = i['properties']['NAME_L']
```

Esta operación crea una propiedad `id` para cada elemento geográfico.

El identificador se obtiene de:

```python
i['properties']['NAME_L']
```

**Concepto importante:** el identificador permite relacionar cada región del archivo GeoJSON con su correspondiente registro en el DataFrame.

## 14.4. Cargar los datos estadísticos

Los datos de población se cargan mediante Pandas:

```python
pop_df = pd.read_csv(
    'data/indiana_population_by_county.csv'
)
```

El DataFrame contiene información de población asociada a cada condado.

Para consultar un condado concreto:

```python
pop_df[
    pop_df['County'] == 'Steuben'
]
```

## 14.5. Crear el mapa coroplético

La clase utilizada es:

```python
folium.Choropleth()
```

### Parámetros principales

| Parámetro | Descripción |
|---|---|
| `geo_data` | Información geográfica del archivo GeoJSON. |
| `name` | Nombre de la capa. |
| `data` | DataFrame con los datos estadísticos. |
| `columns` | Columnas que contienen los identificadores y los valores. |
| `key_on` | Ruta dentro del GeoJSON utilizada para relacionar los datos. |
| `fill_color` | Paleta de colores utilizada para rellenar las regiones. |
| `fill_opacity` | Opacidad del relleno. |
| `line_opacity` | Opacidad de las líneas que delimitan las regiones. |
| `legend_name` | Título de la leyenda. |
| `highlight` | Permite resaltar las regiones al interactuar con ellas. |

### Ejemplo completo

```python
map_choropleth = folium.Map(
    location=[39.77, -86.15],
    zoom_start=7
)

folium.Choropleth(
    geo_data=geo_json_counties,
    name='choropleth',
    data=pop_df,
    columns=[
        'County',
        'Population'
    ],
    key_on='feature.id',
    fill_color='YlGn',
    fill_opacity=0.5,
    line_opacity=0.5,
    legend_name='Population',
    highlight=True
).add_to(map_choropleth)

folium.LayerControl().add_to(map_choropleth)

map_choropleth
```

## 14.6. Relación entre GeoJSON y DataFrame

Uno de los elementos más importantes de un mapa coroplético es la relación entre las geometrías y los datos estadísticos.

En el ejemplo:

```python
columns=['County', 'Population']
```

Indica que:

- `County` contiene los identificadores de los condados.
- `Population` contiene los valores estadísticos que se representarán.

Por otro lado:

```python
key_on='feature.id'
```

Indica dónde se encuentra el identificador correspondiente dentro de la estructura GeoJSON.

La relación es:

```text
DataFrame:
County  <-->  Population

GeoJSON:
feature.id  <-->  feature.geometry
```

Cada condado debe poder relacionarse correctamente con su geometría y su valor de población.

**Concepto fundamental:** si los identificadores no coinciden entre el GeoJSON y el DataFrame, el mapa coroplético no podrá asociar correctamente los valores a las regiones.

---

# 15. Mapas de calor (Heat Maps)

Un mapa de calor permite representar la concentración o intensidad de determinados fenómenos geográficos.

En lugar de representar cada ubicación únicamente mediante un marcador independiente, se utiliza una representación visual basada en la intensidad de los datos.

Los mapas de calor son especialmente útiles para identificar:

- Concentraciones de población.
- Zonas con mayor actividad.
- Distribución de eventos.
- Concentración de puntos geográficos.
- Áreas de mayor intensidad de una variable.

En Folium se utiliza:

```python
plugins.HeatMap()
```

## 15.1. Estructura de los datos

El plugin `HeatMap` recibe una lista de puntos geográficos.

Cada punto puede contener tres valores:

```python
[latitude, longitude, intensity]
```

Donde:

- `latitude`: latitud del punto.
- `longitude`: longitud del punto.
- `intensity`: intensidad asociada a la ubicación.

El tercer valor permite representar diferencias de magnitud entre los puntos.

## 15.2. Obtener coordenadas mediante Geocoder

En el ejemplo del notebook se obtienen las coordenadas de diferentes ciudades estadounidenses.

```python
new_york_city = geocoder.osm(
    'New York City, New York'
)

los_angeles = geocoder.osm(
    'Los Angeles, California'
)

chicago = geocoder.osm(
    'Chicago, Illinois'
)

houston = geocoder.osm(
    'Houston, Texas'
)
```

El mismo procedimiento se utiliza para otras ciudades.

## 15.3. Crear puntos con intensidad

En el notebook se utiliza la población de cada ciudad como intensidad.

Por ejemplo:

```python
new_york_city_latlng = [
    new_york_city.lat,
    new_york_city.lng,
    8398748 / 1000
]
```

La población se divide entre 1.000 para reducir la magnitud de los valores y facilitar la visualización de los puntos de calor.

Se aplica el mismo procedimiento a las demás ciudades.

Posteriormente se agrupan los puntos en una lista:

```python
large_cities = [
    new_york_city_latlng,
    los_angeles_latlng,
    chicago_latlng,
    houston_latlng,
    phoenix_latlng,
    philadelphia_latlng,
    san_antonio_latlng,
    san_diego_latlng,
    dallas_latlng,
    san_jose_latlng
]
```

## 15.4. Crear el mapa de calor

```python
map_heatmap = folium.Map(
    [40, -99],
    tiles='CartoDB Positron',
    zoom_start=4
)

plugins.HeatMap(
    large_cities
).add_to(map_heatmap)

map_heatmap
```

**Concepto importante:** los mapas de calor permiten representar visualmente la intensidad de una variable asociada a diferentes coordenadas geográficas.

---

# 16. Mapas de calor temporales (HeatMapWithTime)

Folium también permite representar mapas de calor que evolucionan a lo largo del tiempo.

Para ello se utiliza:

```python
plugins.HeatMapWithTime()
```

Esta herramienta permite visualizar cómo cambia la distribución espacial de los datos en diferentes instantes temporales.

## 16.1. Estructura de los datos

A diferencia del mapa de calor convencional, el mapa temporal necesita una estructura de datos organizada por periodos.

El formato utilizado en el notebook es:

```text
[
    [
        [latitude, longitude],
        [latitude, longitude],
        ...
    ],
    [
        [latitude, longitude],
        [latitude, longitude],
        ...
    ],
    ...
]
```

Cada bloque representa un periodo temporal y contiene las coordenadas de los puntos correspondientes a ese periodo.

En términos generales:

```python
[
    datos_periodo_1,
    datos_periodo_2,
    datos_periodo_3
]
```

## 16.2. Generar datos de ejemplo

El notebook utiliza NumPy para generar datos aleatorios:

```python
heatmap_time_data = (
    np.random.random((100, 20, 2))
    + np.array([[39, -98]])
).tolist()
```

La estructura generada contiene:

- 100 periodos.
- 20 puntos por periodo.
- 2 coordenadas por punto.

Las coordenadas se generan alrededor de una ubicación de referencia.

El método `tolist()` convierte la estructura de NumPy en listas de Python.

## 16.3. Crear fechas asociadas a los datos

Para representar los diferentes periodos se genera una lista de fechas:

```python
heatmap_time_dates = [
    d.strftime('%Y-%m-%d')
    for d in pd.date_range(
        '20160101',
        periods=len(heatmap_time_data)
    )
]
```

En este ejemplo:

- `pd.date_range()` genera una secuencia de fechas.
- `periods` determina el número de fechas.
- `strftime('%Y-%m-%d')` transforma cada fecha en una cadena con formato año-mes-día.

Cada conjunto de datos queda asociado a una fecha.

## 16.4. Crear el mapa temporal

```python
map_heatmap_time = folium.Map(
    [39, -98],
    tiles='CartoDB Dark_Matter',
    zoom_start=6
)

heatmap_time_plugin = plugins.HeatMapWithTime(
    heatmap_time_data,
    index=heatmap_time_dates
)

heatmap_time_plugin.add_to(
    map_heatmap_time
)

map_heatmap_time
```

El parámetro `index` permite proporcionar las fechas correspondientes a cada conjunto de datos.

**Concepto importante:** `HeatMapWithTime` amplía los mapas de calor tradicionales incorporando una dimensión temporal que permite observar la evolución de los fenómenos geográficos.

---

# 17. Herramienta de coordenadas geográficas (Latitude and Longitude Tool)

Folium permite incorporar una herramienta que muestra las coordenadas geográficas de una ubicación al hacer clic sobre el mapa.

Para ello se utiliza:

```python
folium.LatLngPopup()
```

### Ejemplo

```python
map_lat_long = folium.Map(
    location=[38, -98],
    zoom_start=4
)

map_lat_long.add_child(
    folium.LatLngPopup()
)

map_lat_long
```

Al hacer clic sobre cualquier punto del mapa se muestran sus coordenadas:

- Latitud.
- Longitud.

**Utilidad:** esta herramienta permite identificar las coordenadas exactas de una ubicación sin tener que introducirlas manualmente.

---

# 18. Herramienta de medición (Measure Control)

Folium incorpora un plugin que permite medir distancias directamente sobre el mapa.

Se utiliza:

```python
plugins.MeasureControl()
```

Esta herramienta permite seleccionar puntos sobre el mapa y calcular distancias entre ellos.

## Parámetros principales

| Parámetro | Descripción |
|---|---|
| `position` | Posición del control en el mapa. |
| `active_color` | Color utilizado durante la medición activa. |
| `completed_color` | Color de la medición finalizada. |
| `primary_length_unit` | Unidad principal de longitud. |

## Ejemplo

```python
map_measure = folium.Map(
    [40, -100],
    zoom_start=4
)

measure_control = plugins.MeasureControl(
    position='topleft',
    active_color='red',
    completed_color='red',
    primary_length_unit='meters'
)

map_measure.add_child(
    measure_control
)

map_measure
```

En este ejemplo:

- El control aparece en la esquina superior izquierda.
- Las mediciones utilizan el color rojo.
- La unidad principal de longitud es el metro.

**Concepto importante:** MeasureControl permite calcular distancias geográficas de manera interactiva directamente sobre el mapa.

---

# 19. Mapas dobles (Dual Map)

Folium dispone de un plugin que permite visualizar dos mapas simultáneamente.

Se utiliza:

```python
plugins.DualMap()
```

Esta herramienta resulta especialmente útil para comparar diferentes representaciones cartográficas de una misma zona.

Por ejemplo:

- Comparar diferentes estilos de mapas.
- Comparar distintas capas cartográficas.
- Analizar diferencias entre representaciones del territorio.

## Ejemplo

```python
map_dual = plugins.DualMap(
    location=[40, -98],
    tiles=None,
    zoom_start=4
)
```

Se establece:

- `location`: centro geográfico de los mapas.
- `tiles=None`: permite añadir posteriormente las capas cartográficas deseadas.
- `zoom_start`: nivel de zoom inicial.

## Añadir diferentes capas

```python
folium.TileLayer(
    'Stamen Terrain'
).add_to(map_dual)

folium.TileLayer(
    'CartoDB Positron'
).add_to(map_dual)
```

Cada mapa puede utilizar una representación cartográfica diferente.

## Añadir controles

```python
folium.LayerControl().add_to(map_dual)
```

Finalmente:

```python
map_dual
```

**Concepto importante:** DualMap permite comparar visualmente dos mapas de manera simultánea, facilitando el análisis de diferentes representaciones geográficas.

---

# 20. Herramientas de dibujo (Draw)

Folium permite incorporar herramientas interactivas para dibujar elementos geográficos directamente sobre un mapa.

Para ello se utiliza:

```python
plugins.Draw()
```

Estas herramientas permiten dibujar geometrías sobre el mapa y, mediante la configuración adecuada, exportarlas en formato GeoJSON.

## Ejemplo

```python
map_draw = folium.Map(
    location=[40, -99],
    zoom_start=4
)

draw = plugins.Draw(
    export=True
)

draw.add_to(map_draw)

map_draw
```

## Parámetro export

El parámetro:

```python
export=True
```

permite habilitar la exportación de las geometrías dibujadas como un archivo GeoJSON.

## Utilidad de Draw

Esta herramienta permite:

- Dibujar elementos geográficos.
- Crear geometrías directamente sobre el mapa.
- Obtener información geográfica personalizada.
- Exportar las geometrías dibujadas.
- Crear archivos GeoJSON que posteriormente pueden incorporarse a otros mapas.

**Concepto importante:** Draw permite generar información geográfica propia de manera interactiva, sin necesidad de crear manualmente los archivos GeoJSON.

---

# 21. Superposición de imágenes (Overlay Image)

Folium permite incorporar imágenes sobre un mapa geográfico mediante la clase:

```python
folium.raster_layers.ImageOverlay()
```

Esta funcionalidad permite representar imágenes asociadas a una zona geográfica concreta.

La imagen se posiciona dentro de unos límites geográficos definidos mediante coordenadas.

## Parámetros principales

| Parámetro | Descripción |
|---|---|
| `name` | Nombre de la capa de imagen. |
| `image` | Ruta de la imagen que se quiere incorporar. |
| `bounds` | Límites geográficos que determinan dónde se sitúa la imagen. |
| `opacity` | Nivel de transparencia de la imagen. |

## Límites geográficos (Bounds)

El parámetro `bounds` define el área geográfica donde se superpone la imagen.

La estructura utilizada es:

```python
bounds=[
    [lat_min, lon_min],
    [lat_max, lon_max]
]
```

Donde:

- `lat_min`: latitud mínima.
- `lon_min`: longitud mínima.
- `lat_max`: latitud máxima.
- `lon_max`: longitud máxima.

## Ejemplo

```python
map_img_overlay = folium.Map(
    [2, 22],
    zoom_start=3,
    tiles='CartoDB Positron'
)

img_overlay = folium.raster_layers.ImageOverlay(
    name='flags of Africa',
    image='data/flags_of_africa.png',
    bounds=[
        [-38, -28],
        [40, 60]
    ],
    opacity=0.5
)

img_overlay.add_to(map_img_overlay)

folium.LayerControl().add_to(
    map_img_overlay
)

map_img_overlay
```

En este ejemplo se superpone una imagen con las banderas de los países africanos.

La transparencia se establece mediante:

```python
opacity=0.5
```

Esto permite visualizar simultáneamente la imagen y el mapa de fondo.

**Concepto importante:** ImageOverlay permite posicionar imágenes dentro de unos límites geográficos concretos, integrándolas como capas dentro de un mapa interactivo.

---

# 22. Mapas coropléticos de España (Spain Choropleth)

El último apartado del notebook aplica los conocimientos de mapas coropléticos a un conjunto de datos de España.

El objetivo es representar el número total de fallecimientos por comunidad autónoma.

Se utilizan dos fuentes de información:

- `decesos_espania.csv`: contiene los datos estadísticos.
- `provincias-espanolas 2.0.geojson`: contiene la información geográfica de las comunidades autónomas.

## 22.1. Cargar los datos

Se utiliza Pandas para importar el archivo CSV:

```python
import pandas as pd

data_total_mean = pd.read_csv(
    'data/decesos_espania.csv',
    sep=';'
)
```

El parámetro:

```python
sep=';'
```

indica que el separador de las columnas del archivo CSV es el punto y coma.

## 22.2. Crear el mapa inicial

```python
m = folium.Map(
    location=[42.1257, -8],
    zoom_start=5
)
```

Se establece el centro geográfico del mapa y su nivel de zoom inicial.

## 22.3. Añadir diferentes capas cartográficas

El notebook incorpora diferentes tipos de mapas de fondo:

```python
tiles = [
    'stamenwatercolor',
    'cartodbpositron',
    'openstreetmap',
    'stamenterrain'
]

for tile in tiles:

    folium.TileLayer(tile).add_to(m)
```

Esto permite disponer de diferentes estilos cartográficos que pueden seleccionarse mediante el control de capas.

## 22.4. Crear el mapa coroplético

Se utiliza el método:

```python
m.choropleth()
```

### Ejemplo completo

```python
m.choropleth(
    geo_data='data/provincias-espanolas 2.0.geojson',
    name='choropleth',
    data=data_total_mean,
    columns=[
        'Comunidad Autónoma',
        'Todas las causas'
    ],
    key_on='feature.properties.ccaa',
    fill_color='BuPu',
    fill_opacity=0.7,
    line_opacity=0.2,
    legend_name='Decesos por comunidad autonoma'
)

folium.LayerControl().add_to(m)

m
```

## 22.5. Relación entre los datos y el GeoJSON

Este ejemplo sigue el mismo principio utilizado en el mapa coroplético de Indiana.

La relación se establece mediante:

```python
columns=[
    'Comunidad Autónoma',
    'Todas las causas'
]
```

Donde:

- `Comunidad Autónoma`: identifica cada territorio.
- `Todas las causas`: contiene el valor estadístico que se representará.

Por otro lado:

```python
key_on='feature.properties.ccaa'
```

Indica que la identificación de cada territorio se encuentra en la propiedad `ccaa` de las entidades del GeoJSON.

Por tanto, se establece una correspondencia entre:

```text
CSV:
Comunidad Autónoma
        |
        v
Valor estadístico:
Todas las causas

GEOJSON:
feature.properties.ccaa
        |
        v
Geometría de la comunidad autónoma
```

## 22.6. Personalización visual

En este ejemplo se utiliza:

```python
fill_color='BuPu'
```

Esta paleta utiliza tonalidades azules y púrpuras.

También se establecen:

```python
fill_opacity=0.7
line_opacity=0.2
```

Que controlan respectivamente la opacidad del relleno y de las líneas de separación.

La leyenda se define mediante:

```python
legend_name='Decesos por comunidad autonoma'
```

**Concepto importante:** este último ejercicio demuestra cómo aplicar los mapas coropléticos a datos estadísticos reales, relacionando información territorial de un GeoJSON con valores almacenados en un CSV.

---

# 23. Archivos de datos utilizados en el notebook

El notebook utiliza diferentes archivos externos para construir las representaciones geográficas.

| Archivo | Formato | Utilidad |
|---|---|---|
| `indiana_outline_map.geojson` | GeoJSON | Representación del contorno geográfico de Indiana. |
| `sales_region1.geojson` | GeoJSON | Información geográfica de la región comercial 1. |
| `sales_region2.geojson` | GeoJSON | Información geográfica de la región comercial 2. |
| `sales_region3.geojson` | GeoJSON | Información geográfica de la región comercial 3. |
| `geojson_indianacounties.geojson` | GeoJSON | Geometrías de los condados de Indiana. |
| `indiana_population_by_county.csv` | CSV | Datos de población por condado de Indiana. |
| `flags_of_africa.png` | PNG | Imagen de las banderas de los países africanos. |
| `decesos_espania.csv` | CSV | Datos estadísticos de fallecimientos en España. |
| `provincias-espanolas 2.0.geojson` | GeoJSON | Información geográfica utilizada para representar los datos por comunidad autónoma. |

## Formatos geográficos y estadísticos

### GeoJSON

Formato utilizado para almacenar información geográfica estructurada.

Permite representar geometrías y propiedades asociadas a diferentes elementos territoriales.

### CSV

Formato de texto utilizado para almacenar información tabular.

En este notebook se utiliza para guardar datos estadísticos asociados a territorios.

### PNG

Formato de imagen utilizado para incorporar elementos gráficos sobre un mapa mediante `ImageOverlay`.

---

# 24. Resumen de las principales clases y funciones de Folium

La siguiente tabla recoge las principales clases y métodos utilizados a lo largo del notebook.

| Clase o función | Utilidad |
|---|---|
| `folium.Map()` | Crear un mapa interactivo. |
| `map.save()` | Guardar un mapa como archivo HTML. |
| `folium.TileLayer()` | Añadir capas cartográficas. |
| `folium.LayerControl()` | Incorporar controles para activar y desactivar capas. |
| `plugins.MiniMap()` | Incorporar un minimapa. |
| `plugins.Fullscreen()` | Permitir visualizar el mapa a pantalla completa. |
| `folium.Marker()` | Añadir marcadores geográficos. |
| `folium.Icon()` | Personalizar los iconos de los marcadores. |
| `plugins.BeautifyIcon()` | Crear marcadores personalizados y numerados. |
| `folium.Circle()` | Crear círculos con radio definido en metros. |
| `folium.CircleMarker()` | Crear círculos con radio definido en píxeles. |
| `folium.PolyLine()` | Dibujar líneas que conectan diferentes coordenadas. |
| `plugins.AntPath()` | Representar rutas mediante líneas animadas. |
| `folium.GeoJson()` | Incorporar información geográfica GeoJSON. |
| `folium.FeatureGroup()` | Agrupar elementos geográficos. |
| `plugins.FeatureGroupSubGroup()` | Crear subgrupos dentro de grupos principales. |
| `folium.Choropleth()` | Crear mapas coropléticos. |
| `plugins.HeatMap()` | Crear mapas de calor. |
| `plugins.HeatMapWithTime()` | Crear mapas de calor temporales. |
| `folium.LatLngPopup()` | Mostrar coordenadas geográficas al hacer clic. |
| `plugins.MeasureControl()` | Medir distancias sobre el mapa. |
| `plugins.DualMap()` | Visualizar dos mapas simultáneamente. |
| `plugins.Draw()` | Dibujar geometrías sobre un mapa. |
| `folium.raster_layers.ImageOverlay()` | Superponer imágenes sobre un mapa. |

---

# 25. Conceptos fundamentales que hay que recordar

## 25.1. Coordenadas geográficas

Todas las ubicaciones utilizadas por Folium se representan mediante coordenadas geográficas.

La estructura habitual es:

```python
[latitude, longitude]
```

Es fundamental respetar el orden de las coordenadas.

## 25.2. Capas cartográficas

Los mapas pueden incorporar diferentes capas de representación visual.

Se utilizan para cambiar el estilo del mapa de fondo o añadir información geográfica adicional.

La función principal para incorporar capas es:

```python
folium.TileLayer()
```

Para gestionar las capas:

```python
folium.LayerControl()
```

## 25.3. Marcadores

Los marcadores permiten representar ubicaciones concretas.

Pueden personalizarse mediante iconos, colores, popups y tooltips.

Se pueden crear individualmente o automatizar utilizando DataFrames y diccionarios.

## 25.4. Representación de superficies

Folium permite representar áreas mediante círculos, geometrías GeoJSON e imágenes superpuestas.

Estas funcionalidades permiten pasar de una representación puntual a una representación espacial más compleja.

## 25.5. Datos geográficos y datos estadísticos

Uno de los conceptos más importantes del notebook es la integración de información geográfica con información estadística.

Para construir mapas coropléticos se necesitan:

- Geometrías territoriales almacenadas en GeoJSON.
- Datos estadísticos almacenados en un DataFrame.
- Un identificador común que permita relacionar ambas fuentes.

## 25.6. Mapas de calor

Los mapas de calor permiten visualizar la concentración e intensidad de fenómenos geográficos.

Pueden utilizar coordenadas e intensidades para representar diferentes magnitudes.

También pueden incorporar una dimensión temporal.

## 25.7. Plugins

Los plugins amplían las funcionalidades básicas de Folium.

Permiten incorporar herramientas de medición, dibujo, navegación, comparación de mapas y visualización de datos.

---

# 26. Esquema general de trabajo con Folium

El flujo de trabajo habitual para construir un mapa interactivo con Folium puede resumirse en los siguientes pasos:

1. **Importar las librerías necesarias.**

   ```python
   import folium
   from folium import plugins
   import pandas as pd
   ```

2. **Obtener o preparar los datos geográficos.**

   Los datos pueden proceder de coordenadas conocidas, servicios de geocodificación, archivos GeoJSON o DataFrames.

3. **Crear el mapa inicial.**

   ```python
   m = folium.Map(
       location=[latitude, longitude],
       zoom_start=10
   )
   ```

4. **Incorporar las capas cartográficas necesarias.**

   ```python
   folium.TileLayer(
       'OpenStreetMap'
   ).add_to(m)
   ```

5. **Añadir los elementos geográficos.**

   Según las necesidades del análisis, se pueden incorporar marcadores, rutas, círculos, polígonos, mapas de calor o mapas coropléticos.

6. **Incorporar controles y herramientas interactivas.**

   ```python
   folium.LayerControl().add_to(m)
   ```

7. **Visualizar el mapa.**

   ```python
   m
   ```

8. **Guardar el resultado.**

   ```python
   m.save('mapa_interactivo.html')
   ```

---

# 27. Conclusión

Folium es una herramienta muy versátil para la creación de mapas interactivos utilizando Python.

Su principal potencial reside en la posibilidad de combinar información geográfica con datos estadísticos y representarlos de forma visual mediante mapas dinámicos.

Principales funcionalidades de la librería:

- Creación y personalización de mapas.
- Selección de diferentes estilos cartográficos.
- Incorporación de marcadores convencionales y personalizados.
- Geocodificación de direcciones.
- Automatización de marcadores utilizando Pandas.
- Representación de círculos y rutas.
- Incorporación de archivos GeoJSON.
- Organización de información geográfica mediante grupos y subgrupos.
- Creación de mapas coropléticos.
- Representación de datos mediante mapas de calor.
- Visualización de mapas de calor temporales.
- Incorporación de herramientas de coordenadas y medición.
- Comparación de mapas mediante DualMap.
- Creación y exportación de geometrías mediante Draw.
- Superposición de imágenes georreferenciadas.

La combinación de Folium con Pandas, NumPy, Geocoder y GeoJSON permite desarrollar visualizaciones geográficas que facilitan el análisis espacial y la interpretación de datos territoriales.

**La idea fundamental es que Folium permite transformar datos geográficos y estadísticos en mapas interactivos, personalizables y exportables a HTML.**








<hr>








