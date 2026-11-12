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
