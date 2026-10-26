# Data_analysis
Data Analysis https://formacion.thebridge.tech/ 

![Data Science con IA](https://raw.githubusercontent.com/aupatxus/ONLINE_DS_THEBRIDGE_GitHub/refs/heads/main/Vital%20LANBIDE.png)

NumPy (Numerical Python) es la librería fundamental en Python para la computación científica y el análisis de datos. Su gran ventaja es que introduce los arrays, estructuras de datos que permiten almacenar colecciones de elementos del mismo tipo de forma extremadamente rápida y eficiente, superando por mucho el rendimiento de las listas nativas de Python.



1. Listas y Matrices

Las listas de Python son muy flexibles porque pueden guardar cualquier tipo de dato (números, texto, booleanos combinados). Sin embargo, esa flexibilidad las hace lentas para el cálculo matemático estructurado.
Una matriz es una cuadrícula bidimensional organizada en filas y columnas. En Python básico, las matrices se representan como "listas de listas" (por ejemplo, [[1, 2], [3, 4]]), pero operar matemáticamente con ellas requiere bucles for, lo cual es ineficiente y tedioso de programar.



2. NumPy

NumPy resuelve este problema introduciendo el ndarray (array N-dimensional). A diferencia de las listas:
- Son homogéneos: Todos los elementos dentro de un array deben ser estrictamente del mismo tipo de dato.
- Memoria eficiente: Se almacenan en bloques de memoria contiguos, lo que permite realizar operaciones matemáticas directamente sobre miles de datos a la vez (proceso llamado vectorización) sin usar bucles.
Para usarlo, siempre debes importarlo bajo el alias estándar np:
````
import numpy as np
````


3. Creación de arrays

Existen múltiples formas de crear arrays en NumPy dependiendo de lo que necesites:
- Desde una lista:
````
vector = np.array([1, 2, 3]) # 1 Dimensión
matriz = np.array([[1, 2], [3, 4]]) # 2 Dimensiones
````

- Con valores predefinidos:
````
ceros = np.zeros((3, 4))   # Crea una matriz de 3x4 llena de ceros (0.0)
unos = np.ones((2, 2))     # Crea una matriz de 2x2 llena de unos (1.0)
vacia = np.full((2, 3), 7) # Crea una matriz de 2x3 llena del número 7
````

- Con secuencias numéricas:
````
rango = np.arange(0, 10, 2)  # De 0 a 9 saltando de 2 en 2 -> [0, 2, 4, 6, 8]
lineal = np.linspace(0, 1, 5) # 5 números equiespaciados entre 0 y 1 -> [0. , 0.25, 0.5 , 0.75, 1.]
````

- Con números aleatorios:
````
aleatorio = np.random.rand(3, 3) # Matriz 3x3 con números decimales aleatorios entre 0 y 1
````



4. Atributos del array

Cuando tienes un array, puedes inspeccionar sus propiedades utilizando sus atributos nativos (nota que no llevan paréntesis al final):
- ndim: Indica el número de dimensiones (ejes). Un vector tiene 1, una tabla tiene 2.
- shape: Devuelve una tupla indicando el tamaño de cada dimensión (filas, columnas).
- size: Indica el número total de elementos que contiene el array.
- dtype: Muestra el tipo de datos de los elementos internos.


````
mi_matriz = np.array([[1, 2, 3], [4, 5, 6]])
print(mi_matriz.ndim)  # 2
print(mi_matriz.shape) # (2, 3) -> 2 filas y 3 columnas
print(mi_matriz.size)  # 6
````



5. Indexado

El indexado sirve para seleccionar un único elemento del array. Al igual que en Python, el conteo empieza en 0.
- En 1D, funciona igual que las listas: array[0].
- En 2D, se utiliza la nomenclatura [fila, columna].

````
matriz = np.array([[10, 20], [30, 40]])
print(matriz[0, 1]) # Elemento en fila 0, columna 1 -> 20
print(matriz[1, 0]) # Elemento en fila 1, columna 0 -> 30
````



6. Slicing y subarrays

El slicing (rebanado) permite extraer fragmentos o secciones del array usando el formato [inicio:fin:paso].
Si es una matriz bidimensional, se separa la rebanada de filas y columnas con una coma: [filas_inicio:filas_fin, columnas_inicio:columnas_fin].
````
matriz = np.array([[1, 2, 3], , 
                   [7, 8, 9]])

# Extraer las primeras dos filas y las dos primeras columnas
sub_matriz = matriz[0:2, 0:2]
# Resultado: [[1, 2], 
#]

# Extraer una fila completa usando ':'
primera_fila = matriz[0, :] # [1, 2, 3]
````



7. Reshape

El método .reshape() te permite cambiar la forma (filas y columnas) de un array sin modificar sus datos internos. La única condición obligatoria es que el tamaño total (size) debe mantenerse igual.

````
vector = np.array([1, 2, 3, 4, 5, 6]) # Tamaño 6
matriz_nueva = vector.reshape((2, 3)) # Transforma a 2 filas y 3 columnas

print(matriz_nueva)
# [[1, 2, 3],
#]
````



8. Tipos de los datos

Como NumPy es homogéneo, asigna tipos fijos muy específicos para optimizar la memoria. Algunos de los más comunes son int32, int64, float64, y bool.
Puedes forzar el tipo al crear el array o cambiarlo después usando .astype():

````
# Crear forzando números flotantes (decimales)
enteros = np.array([1, 2, 3], dtype='float64') # [1., 2., 3.]

# Convertir un array existente de decimales a enteros
decimales = np.array([1.9, 2.5, 3.1])
enteros_nuevos = decimales.astype('int32') # [1, 2, 3] (Trunca el decimal, no redondea)
````



9. Concatenado

Unir múltiples arrays en uno solo se logra mediante np.concatenate(). En matrices bidimensionales, debes especificar el eje (axis):
- axis=0: Une verticalmente (añade filas).
- axis=1: Une horizontalmente (añade columnas).

````
a = np.array([[1, 2]])
b = np.array([[3, 4]])

# Concatenar verticalmente
vertical = np.concatenate([a, b], axis=0)
# [[1, 2],
#]

# Concatenar horizontalmente
horizontal = np.concatenate([a, b], axis=1)
# [[1, 2, 3, 4]]
````



10. Sustitución

Cambiar el valor de elementos específicos es muy directo asignando un nuevo valor a la posición indexada o al subarray seleccionado.

````
x = np.array([10, 20, 30])
x[1] = 99 # Sustituye el 20 por 99 -> [10, 99, 30]

# Sustitución masiva con condiciones (Filtrado booleano)
edades = np.array([15, 25, 12, 40])
edades[edades < 18] = 0 # Sustituye cualquier menor de 18 por 0 -> [0, 25, 0, 40]
````



11. Copias

¡Cuidado aquí! Si haces un slicing (sub = matriz[0:2]) y modificas sub, la matriz original también cambiará. En NumPy, los subarrays son solo "vistas" de los datos originales para ahorrar memoria.
Si quieres modificar un fragmento sin alterar el original, debes usar explícitamente .copy():

````
original = np.array([1, 2, 3])

# Copia real e independiente
copia_segura = original.copy()
copia_segura[0] = 99 

print(original)     # [1, 2, 3] (Se mantiene intacto)
print(copia_segura) # [99, 2, 3]
````



12. Splitting

El splitting es la operación inversa a la concatenación: divide un único array en múltiples arrays pequeños. Se realiza con np.split(), np.vsplit() (corte vertical) o np.hsplit() (corte horizontal).

````
datos = np.array([10, 20, 30, 40, 50, 60])
# Dividir en el índice 2 y en el índice 4
parte1, parte2, parte3 = np.split(datos, [2, 4])

print(parte1) # [10, 20]
print(parte2) # [30, 40]
print(parte3) # [50, 60]
````



13. Agregaciones

Las agregaciones son funciones matemáticas rápidas integradas que resumen o calculan estadísticas sobre los elementos de un array.
- np.sum(): Suma todos los elementos.
- np.min() / np.max(): Encuentra los valores mínimos y máximos.
- np.mean(): Calcula la media (promedio).
- np.std(): Calcula la desviación estándar.
Puedes aplicarlos a todo el array o a un eje específico (por ejemplo, calcular la suma solo de cada columna usando axis=0).

````
numeros = np.array([[1, 2], [3, 4]])

print(np.sum(numeros))          # 10 (Suma total)
print(np.mean(numeros, axis=0)) # [2. , 3.] (Media de cada columna)

````

