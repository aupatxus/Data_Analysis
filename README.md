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


## 1. Creación de DataFrames

Permite definir estructuras de datos bidimensionales con etiquetas en filas y columnas. 
* Por columnas: df = pd.DataFrame({"a":, "b": [7, 8, 9]}, index=[1, 2, 3]) -> Especifica valores columna por columna.
* Por filas: df = pd.DataFrame([[4, 7, 10], [5, 8, 11]], index=[1, 2], columns=['a', 'b', 'c']) -> Especifica valores fila por fila.
* Con MultiIndex (Índices jerárquicos): df = pd.DataFrame(data, index=pd.MultiIndex.from_tuples([('d', 1), ('d', 2)], names=['n', 'v'])). 

## 2. Remodelación de Datos (Reshaping)

Cambia la disposición, ordenación, índices y nombres de las tablas. 
* pd.melt(df): Reúne columnas y las transforma en filas (unpivot).
* df.pivot(columns='var', values='val'): Expande filas y las transforma en columnas (pivot).
* pd.concat([df1, df2]): Concatena filas de varios DataFrames.
* pd.concat([df1, df2], axis=1): Concatena columnas de varios DataFrames.
* df.sort_values('col'): Ordena las filas por los valores de una columna (menor a mayor). Usa ascending=False para orden inverso.
* df.sort_index(): Ordena el índice del DataFrame.
* df.reset_index(): Restablece el índice a números secuenciales, moviendo el índice anterior a una columna.
* df.rename(columns={'antiguo': 'nuevo'}): Renombra las columnas.
* df.drop(columns=['col1', 'col2']): Elimina las columnas indicadas. 

## 3. Filtrado y Subconjuntos (Subsets)

Selección de observaciones (filas), variables (columnas) o elementos específicos. 

Filtrado de Filas (Subsets de observaciones)

* df[df.Length > 7]: Extrae filas que cumplen un criterio lógico.
* df.drop_duplicates(): Elimina filas duplicadas.
* df.head(n) / df.tail(n): Selecciona las primeras o últimas n filas.
* df.sample(frac=0.5) / df.sample(n=10): Selecciona una fracción aleatoria o un número fijo n de filas.
* df.nlargest(n, 'col') / df.nsmallest(n, 'col'): Selecciona y ordena las n entradas más grandes o más pequeñas.
* Uso de .query(): Permite expresiones booleanas en cadena de texto, ej: df.query('Length > 7 and Width < 8') o df.query('Name.str.startswith("abc")', engine="python"). 

Filtrado de Columnas (Subsets de variables)

* df[['col1', 'col2']]: Selecciona múltiples columnas por nombre.
* df['col'] o df.col: Selecciona una única columna como Series.
* df.filter(regex='regex'): Selecciona columnas cuyos nombres coinciden con una expresión regular. 

Subconjuntos combinados (Filas y Columnas)

* df.iloc[10:20]: Selecciona las filas de la posición 10 a la 20.
* df.iloc[:, [1, 2, 5]]: Selecciona las columnas en las posiciones numéricas 1, 2 y 5.
* df.loc[:, 'x2':'x4']: Selecciona todas las columnas entre 'x2' y 'x4' inclusive.
* df.loc[df['a'] > 10, ['a', 'c']]: Selecciona las filas que cumplen la condición, y solo las columnas 'a' y 'c'.
* df.at[4, 'A'] / df.iat[1, 2]: Accede de manera rápida a un único valor por etiqueta o por posición de índice, respectivamente. 

## 4. Lógica y Expresiones Regulares en Python/Pandas

* Operadores lógicos: < (menor), > (mayor), == (igual), != (diferente), <= , >=.
* Funciones lógicas: df.column.isin(valores) (pertenencia a grupo), pd.isnull(obj) (es NaN), pd.notnull(obj) (no es NaN).
* Conectores lógicos: & (and), | (or), ~ (not), ^ (xor), df.any() (alguno), df.all() (todos).
* Ejemplos Regex: '\.' (contiene un punto), 'Length$' (termina en 'Length'), '^Sepal' (empieza por 'Sepal'), '^x[1-5]$' (empieza con 'x' y termina en número del 1 al 5), '^(?!Species$).*' (cualquier cadena excepto 'Species'). 

## 5. Encadenamiento de Métodos (Method Chaining)

Dado que la mayoría de los métodos de Pandas devuelven un DataFrame, se pueden enlazar operaciones consecutivas entre paréntesis para mejorar la legibilidad del código: 
````
df = (pd.melt(df)
     .rename(columns={'variable': 'var', 'value': 'val'})
     .query('val >= 200'))
````

## 6. Creación de Nuevas Columnas

* df.assign(Area=lambda df: df.Length * df.Height): Calcula e inserta una o más columnas nuevas devolviendo un DataFrame. 
* df['Volume'] = df.Length * df.Height * df.Depth: Añade directamente una nueva columna al DataFrame actual. 
* pd.qcut(df.col, n, labels=False): Divide o agrupa una columna en n cuantiles discretos. 
* Funciones Vectoriales: Operan de manera eficiente en columnas completas o Series:
	* max(axis=1) / min(axis=1): Máximo o mínimo por filas (horizontal).
	* clip(lower=-10, upper=10): Recorta y limita los valores dentro de los umbrales indicados.
	* abs(): Valor absoluto. 

## 7. Tratamiento de Datos Faltantes (Missing Data)

* df.dropna(): Elimina cualquier fila que contenga algún valor nulo (NA/null).
* df.fillna(value): Reemplaza todos los valores nulos (NA/null) por el valor especificado. 

## 8. Resumen Estadístico y Exploración (Summarize Data)

* df['w'].value_counts(): Cuenta las frecuencias de cada valor único en una columna.
* len(df): Devuelve el número de filas.
* df.shape: Tupla con el formato (número_de_filas, número_de_columnas).
* df['w'].nunique(): Cuenta la cantidad de valores distintos/únicos en una columna.
* df.describe(): Genera estadísticas descriptivas básicas para cada columna numérica.
* df.info(): Imprime un resumen conciso de la estructura del DataFrame.
* df.memory_usage(): Muestra el uso de memoria de cada columna.
* df.dtypes: Muestra los tipos de datos de cada columna.
* Funciones de agregación comunes: sum(), count() (ignora nulos), median(), quantile([0.25, 0.75]), min(), max(), mean(), var(), std().
* apply(function): Aplica una función personalizada a lo largo del objeto. 

## 9. Agrupación de Datos (Group Data)

* df.groupby(by="col"): Crea un objeto agrupado por los valores de la columna "col". 
* df.groupby(level="ind"): Agrupa por un nivel específico de un MultiIndex llamado "ind". 
* Funciones para GroupBy:
	* size(): Devuelve el tamaño (conteo) de cada grupo.
	* agg(function): Agrega los grupos aplicando una función específica. 
* Funciones por grupo (mantiene la longitud original del DataFrame):
	* shift(1) / shift(-1): Desplaza o retrasa los valores en una posición.
	* rank(method='dense') / rank(method='min') / rank(method='first') / rank(pct=True): Calcula los rangos de los elementos lidiando de formas distintas con los empates.
	* cumsum() / cummax() / cummin() / cumprod(): Suma, máximo, mínimo o producto acumulado, respectivamente. 

## 10. Ventanas de Tiempo y Acumulados (Windows)

* df.expanding(): Devuelve un objeto de expansión para aplicar funciones de resumen de manera acumulativa.
* df.rolling(n): Devuelve un objeto de ventana móvil para aplicar funciones de resumen en bloques fijos de tamaño n. 

## 11. Combinación de Datasets (Joins)

Permite unir dos tablas (adf y bdf) en función de una columna común (on='x1'). 

Joins Estándar

* pd.merge(adf, bdf, how='left', on='x1'): Mantiene todas las filas de adf y une las coincidencias de bdf.
* pd.merge(adf, bdf, how='right', on='x1'): Mantiene todas las filas de bdf y une las coincidencias de adf.
* pd.merge(adf, bdf, how='inner', on='x1'): Retiene únicamente las filas con coincidencias en ambas tablas.
* pd.merge(adf, bdf, how='outer', on='x1'): Retiene absolutamente todos los valores y filas de ambas tablas. 

Joins de Filtrado

* adf[adf.x1.isin(bdf.x1)]: Todas las filas de adf que tienen una coincidencia exacta en bdf.
* adf[~adf.x1.isin(bdf.x1)]: Todas las filas de adf que no tienen coincidencia en bdf. 

Operaciones de Conjunto (Set-like Operations)

* pd.merge(ydf, zdf): Filas compartidas en ambos DataFrames (Intersección).
* pd.merge(ydf, zdf, how='outer'): Filas presentes en cualquiera o en ambos DataFrames (Unión).
* pd.merge(ydf, zdf, how='outer', indicator=True).query('_merge == "left_only"').drop(columns=['_merge']): Filas presentes en ydf pero no en zdf (Diferencia de conjuntos). 

## 12. Gráficos y Visualización (Plotting)

Pandas se integra nativamente con Matplotlib para dibujar gráficos de tus DataFrames. 
* df.plot(): Gráfico de líneas estándar. 
* df.plot.scatter(x='w', y='h'): Gráfico de dispersión (Scatter plot).
* df.plot.hist(): Histograma de frecuencias. 
* df.plot.pie(): Gráfico de pastel. 
* df.plot.bar(): Gráfico de barras horizontales/verticales. 
* df.plot.boxplot(): Diagrama de caja y bigotes. 
* df.plot.area(): Gráfico de área. 
* df.plot.hexbin(): Gráfico de compartimentos hexagonales. 
* Argumentos combinables de .plot():
	* subplots=True: Genera gráficos separados para cada columna.
	* title="Texto" o title=['col1', 'col2']: Configura el título general o por subgráfico.
	* stacked=True: Apila las barras de las columnas una encima de la otra (para gráficos de barras o áreas).
	* alpha=0.5: Ajusta la transparencia del color al 50%.
	* cumulative=True: Crea un gráfico acumulativo.
	* bins=30: Define la cantidad de intervalos (para histogramas). 

## 13. Conversión de Tipos de Datos (Changing Type)

* pd.to_numeric(data): Convierte tipos no numéricos a numéricos.
* pd.to_datetime(data): Convierte datos al tipo de fecha datetime.
* pd.to_timedelta(data): Convierte datos al tipo de intervalo timedelta.
* df.astype(type): Fuerza la conversión de los datos a casi cualquier tipo básico o categórico.
* df.infer_objects(): Intenta inferir el tipo de dato idóneo para columnas de tipo objeto.
* df.convert_dtypes(): Convierte las columnas a los mejores tipos posibles soportados de manera inteligente. 

## 14. Operaciones con Cadenas de Texto Vectorizadas (.str)

Operan eficientemente sobre Series completas de tipo string de manera similar a los métodos nativos de Python: 
* s.str.count(pattern): Cuenta las ocurrencias de un patrón.
* s.str.get(index): Extrae el elemento en el índice indicado.
* s.str.join(sep): Concatena los elementos internos usando un separador.
* s.str.title(): Capitaliza la primera letra de cada palabra.
* s.str.len(): Devuelve la longitud de cada string.
* s.str.cat(): Une todos los elementos de la Serie en un único bloque de texto.
* s.str.partition(sep): Divide el texto basándose en la primera aparición del separador.
* s.str.slice(start, stop, step): Corta/Slices cada elemento de texto.
* s.str.replace(pat, rep): Reemplaza patrones definidos mediante texto o Regex.
* s.str.isalnum(): Comprueba si cada carácter es alfanumérico. 

## 15. Fechas y Horas (.dt)

Para Series de tipo datetime, el accesor .dt extrae sus componentes individuales: 
* s.dt.year / s.dt.month / s.dt.day: Extrae el año, mes o día como entero.
* s.dt.quarter: Identifica el trimestre del año en el que cae la fecha.
* s.dt.hour / s.dt.minute / s.dt.second: Extrae la hora, minuto o segundo del registro temporal. 

## 16. Transformación y Mapeado (Mapping)

* s.map(lambda x: 2*x): Aplica una función o diccionario de mapeo a todos los elementos de una Serie individual.
* df.apply(lambda s: s.max() - s.min(), axis=1): Aplica transformaciones avanzadas por columnas o filas (ej. la diferencia entre el máximo y mínimo de cada fila). 

## 17. Entrada y Salida de Datos (Input/Output)

Formatos legibles por humanos (lectura) y optimizados para rendimiento de escala (escritura): 
* Lectura: pd.read_csv(path), pd.read_html(path), pd.read_excel(path), pd.read_sql(path), pd.read_clipboard() (lee el texto copiado en el portapapeles).
* Escritura: df.to_parquet(path), df.to_feather(path), df.to_hdf(path), df.to_clipboard() (copia la tabla al portapapeles de tu ordenador). 

## 18. Opciones de Configuración Global de Pandas

Permite controlar el comportamiento y la visualización de la librería a través de la sintaxis pd.options.display.opcion_name = valor. 

Funciones de gestión de opciones

* get_option(option): Recupera el valor actual de una opción.
* set_option(option): Configura una opción.
* reset_option(options): Restablece las opciones a sus configuraciones por defecto.
* describe_option(options): Imprime la descripción detallada de una opción.
* option_context(options): Bloque contextual para ejecutar código con configuraciones temporales que se revierten al salir. 

Opciones más comunes de Visualización (Display options)

* display.max_rows / display.max_columns: Número máximo de filas/columnas a mostrar en la impresión bonita (pretty-print).
* display.expand_frame_repr: Controla si la representación del DataFrame se divide a lo largo de varias páginas.
* display.large_repr: Determina si un DataFrame que excede los límites se trunca o se muestra como un resumen.
* display.precision: Cantidad de decimales de precisión en las salidas.
* display.max_colwidth: Ancho máximo de las columnas; los textos más largos se truncarán.
* display.max_info_columns: Número máximo de columnas mostradas al llamar a df.info().
* display.chop_threshold: Umbral de redondeo a cero para valores numéricos extremadamente pequeños.
* display.colheader_justify: Controla la justificación del texto en las cabeceras de columna. 

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

