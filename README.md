# Data_analysis
Data Analysis https://formacion.thebridge.tech/ 

![Data Science con IA](https://raw.githubusercontent.com/aupatxus/ONLINE_DS_THEBRIDGE_GitHub/refs/heads/main/Vital%20LANBIDE.png)

NumPy (Numerical Python) es la librería fundamental en Python para la computación científica y el análisis de datos. Su gran ventaja es que introduce los arrays, estructuras de datos que permiten almacenar colecciones de elementos del mismo tipo de forma extremadamente rápida y eficiente, superando por mucho el rendimiento de las listas nativas de Python.



## 1. Listas y Matrices

Las listas de Python son muy flexibles porque pueden guardar cualquier tipo de dato (números, texto, booleanos combinados). Sin embargo, esa flexibilidad las hace lentas para el cálculo matemático estructurado.
Una matriz es una cuadrícula bidimensional organizada en filas y columnas. En Python básico, las matrices se representan como "listas de listas" (por ejemplo, [[1, 2], [3, 4]]), pero operar matemáticamente con ellas requiere bucles for, lo cual es ineficiente y tedioso de programar.



## 2. NumPy

NumPy resuelve este problema introduciendo el ndarray (array N-dimensional). A diferencia de las listas:
- Son homogéneos: Todos los elementos dentro de un array deben ser estrictamente del mismo tipo de dato.
- Memoria eficiente: Se almacenan en bloques de memoria contiguos, lo que permite realizar operaciones matemáticas directamente sobre miles de datos a la vez (proceso llamado vectorización) sin usar bucles.
Para usarlo, siempre debes importarlo bajo el alias estándar np:
````
import numpy as np
````



## 3. Creación de arrays

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



## 4. Atributos del array

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



## 5. Indexado

El indexado sirve para seleccionar un único elemento del array. Al igual que en Python, el conteo empieza en 0.
- En 1D, funciona igual que las listas: array[0].
- En 2D, se utiliza la nomenclatura [fila, columna].

````
matriz = np.array([[10, 20], [30, 40]])
print(matriz[0, 1]) # Elemento en fila 0, columna 1 -> 20
print(matriz[1, 0]) # Elemento en fila 1, columna 0 -> 30
````



## 6. Slicing y subarrays

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



## 7. Reshape

El método .reshape() te permite cambiar la forma (filas y columnas) de un array sin modificar sus datos internos. La única condición obligatoria es que el tamaño total (size) debe mantenerse igual.
````
vector = np.array([1, 2, 3, 4, 5, 6]) # Tamaño 6
matriz_nueva = vector.reshape((2, 3)) # Transforma a 2 filas y 3 columnas

print(matriz_nueva)
# [[1, 2, 3],
#]
````



## 8. Tipos de los datos

Como NumPy es homogéneo, asigna tipos fijos muy específicos para optimizar la memoria. Algunos de los más comunes son int32, int64, float64, y bool.
Puedes forzar el tipo al crear el array o cambiarlo después usando .astype():
````
# Crear forzando números flotantes (decimales)
enteros = np.array([1, 2, 3], dtype='float64') # [1., 2., 3.]

# Convertir un array existente de decimales a enteros
decimales = np.array([1.9, 2.5, 3.1])
enteros_nuevos = decimales.astype('int32') # [1, 2, 3] (Trunca el decimal, no redondea)
````



## 9. Concatenado

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



## 10. Sustitución

Cambiar el valor de elementos específicos es muy directo asignando un nuevo valor a la posición indexada o al subarray seleccionado.
````
x = np.array([10, 20, 30])
x[1] = 99 # Sustituye el 20 por 99 -> [10, 99, 30]

# Sustitución masiva con condiciones (Filtrado booleano)
edades = np.array([15, 25, 12, 40])
edades[edades < 18] = 0 # Sustituye cualquier menor de 18 por 0 -> [0, 25, 0, 40]
````



## 11. Copias

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



## 12. Splitting

El splitting es la operación inversa a la concatenación: divide un único array en múltiples arrays pequeños. Se realiza con np.split(), np.vsplit() (corte vertical) o np.hsplit() (corte horizontal).

````
datos = np.array([10, 20, 30, 40, 50, 60])
# Dividir en el índice 2 y en el índice 4
parte1, parte2, parte3 = np.split(datos, [2, 4])

print(parte1) # [10, 20]
print(parte2) # [30, 40]
print(parte3) # [50, 60]
````



## 13. Agregaciones

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



<hr>


## ¿Qué es NumPy?

NumPy (cuya abreviatura significa Numerical Python) es la librería fundamental de Python dedicada al cálculo numérico y al análisis de datos. En el mundo de la programación, si Python es el coche, NumPy es el motor de alta potencia que le permite procesar cantidades masivas de datos a una velocidad increíble.
Fue creada en 2005 por Travis Oliphant para solucionar un gran problema: Python por sí solo es un lenguaje muy amigable y fácil de aprender, pero es relativamente lento cuando tiene que realizar millones de cálculos matemáticos repetitivos. NumPy resolvió esto permitiendo que Python realice operaciones matemáticas complejas casi de forma instantánea.

### La Filosofía Detrás de NumPy: ¿Por qué es tan revolucionario?

Para entender el éxito de NumPy, primero debemos entender su elemento estrella: el Array (o matriz de datos).
Imagina que tienes una lista de la compra con los precios de 5 productos y quieres aplicarles un impuesto del 10%. En Python básico, tendrías que crear un bucle (un comando que va uno por uno leyendo el precio, multiplicándolo y guardándolo). Si en vez de 5 productos tuvieras 10 millones, tu ordenador tardaría bastante tiempo en procesarlo.
NumPy introduce los Ndarrays (bloques de datos estructurados). La magia de estos bloques se basa en tres pilares:
1. Operaciones Vectorizadas (Adiós a los bucles): Con NumPy no tienes que ir fila por fila. Si le dices a NumPy "multiplica esta matriz por 1.10", NumPy multiplica los 10 millones de números todos a la vez en una sola línea de código.
2. Homogeneidad: A diferencia de las listas normales de Python (donde puedes mezclar texto, números y fechas), un array de NumPy exige que todos los elementos sean del mismo tipo (por ejemplo, todos números enteros o todos decimales). Al saber exactamente qué tipo de dato está procesando, el ordenador no tiene que perder tiempo adivinando y organiza la memoria de forma perfecta.
3. Velocidad de Crecimiento en C: Aunque tú escribes en Python de forma sencilla, por detrás, NumPy ejecuta esos cálculos utilizando C y Fortran, lenguajes de programación de bajísimo nivel que funcionan a la velocidad de la luz en el procesador de tu ordenador.

### ¿Cómo funciona en la práctica? (Los 3 Conceptos Clave)

Para dominar NumPy de forma conceptual, solo necesitas entender tres términos:
* Dimensiones (Axes/Ejes):
	* Un array de 1 dimensión es una simple fila de números (un vector, como una lista de temperaturas diarias).
	* Un array de 2 dimensiones es una tabla con filas y columnas (una matriz, como una hoja de cálculo de Excel).
	* Un array de 3 o más dimensiones es como un cubo de datos (un tensor, por ejemplo, una imagen digital, donde tienes filas y columnas de píxeles, y una tercera dimensión para los colores Rojo, Verde y Azul).
* El "Shape" (La Forma): Es la radiografía de tu bloque de datos. Te dice cuántas filas y cuántas columnas tiene exactamente. Por ejemplo, un shape de (3, 5) significa que tienes una tabla con 3 filas y 5 columnas.
* Funciones Universales (ufunc): Son herramientas matemáticas listas para usar que devoran datos. Puedes pedirle a NumPy que calcule la raíz cuadrada, el promedio, el número más alto o la desviación estándar de miles de millones de registros en una milésima de segundo.

### Resumen de su ecosistema: La base de la Inteligencia Artificial

Casi nadie usa NumPy de forma aislada; es la "pieza de LEGO" sobre la que se construye toda la ciencia de datos moderna. Si quieres trabajar en tecnología, verás que:
* Pandas (la librería para manejar tablas de datos y estadísticas) utiliza NumPy por debajo.
* Matplotlib y Seaborn (para dibujar gráficos y mapas) necesitan los datos en formato NumPy.
* Scikit-learn, TensorFlow y PyTorch (los cerebros detrás de la Inteligencia Artificial y el Machine Learning) traducen imágenes, textos y vídeos en arrays de NumPy para poder aprender de ellos.

En conclusión, NumPy no es solo una herramienta de cálculo; es el traductor universal que convierte el caos de datos del mundo real en estructuras de números perfectamente ordenadas, eficientes y ultra rápidas para que tu ordenador pueda analizarlas.



<hr>



## ¿Qué es Pillow?

Pillow es la librería de Python más popular y utilizada para abrir, manipular, editar y guardar imágenes digitales. En el mundo de la programación, si NumPy es el motor matemático experto en calcular números, Pillow es el "estudio de fotografía" que traduce esos números en archivos visuales reales como fotos .jpg, .png, .gif o .webp.
Originalmente nació a partir de un proyecto antiguo llamado PIL (Python Imaging Library), pero como aquel se quedó obsoleto, la comunidad de desarrolladores creó Pillow (que significa Almohada en inglés) como una versión moderna, rápida, fácil de instalar y mantenida al día.

### La conexión perfecta: ¿Por qué Pillow y NumPy trabajan juntos?

En la ciencia de datos y la inteligencia artificial, Pillow y NumPy forman una pareja inseparable debido a cómo entiende las imágenes un ordenador:
1. Pillow abre y guarda la foto: Pillow se encarga del trabajo "sucio" de descodificar formatos. Sabe cómo leer un archivo binario .jpg del disco duro y convertirlo en un objeto visual de Python.
2. NumPy hace la magia matemática: Como vimos anteriormente, una imagen no es más que una gigantesca cuadrícula de píxeles (números). Con una sola línea de código, puedes transformar una imagen de Pillow en un array de NumPy. A partir de ahí, puedes usar NumPy para recortar, aclarar, invertir colores o entrenar una Inteligencia Artificial a la velocidad de la luz.
3. Pillow exporta el resultado: Una vez que NumPy ha terminado de calcular y modificar los números de los píxeles, Pillow toma esa matriz numérica y la vuelve a transformar en una foto real lista para guardar o mostrar en una página web.

### ¿Cómo funciona en la práctica? (Los 3 Pilares de Pillow)

Para dominar Pillow conceptualmente, solo necesitas entender tres funciones esenciales:
* La clase Image: Es el núcleo de la librería. Se utiliza para cargar archivos (Image.open("foto.jpg")), crear imágenes desde cero en un color sólido (Image.new()) o guardarlas aplicando compresión (foto.save("nueva_foto.png")).
* Los Modos de Imagen (Color): Pillow necesita saber cómo interpretar los canales de la foto. Los más comunes son:
	* RGB: Imagen estándar a color (Rojo, Verde, Azul).
	* RGBA: Color estándar pero con un cuarto canal para la Alfa (transparencia).
	* L: Imagen en escala de grises (blanco y negro).
* Filtros y Transformaciones Integrados: Aunque NumPy sirve para hacer modificaciones matemáticas personalizadas, Pillow ya viene con un "menú de botones" listos para usar si solo buscas operaciones típicas de diseño: rotar 90 grados, cambiar el tamaño de los píxeles (redimensionar), enfocar o difuminar (efecto blur).

Ejemplo práctico: Cómo cooperan en el código real

Mira lo sencillo que es abrir una foto con Pillow, convertirla a NumPy para oscurecerla y volverla a guardar como imagen usando ambas librerías combinadas:
````
from PIL import Image
import numpy as np

# 1. Pillow abre la imagen del disco duro
foto_pillow = Image.open("paisaje.jpg")

# 2. Convertimos la foto en una matriz de números de NumPy
matriz_píxeles = np.array(foto_pillow)

# 3. NumPy hace la operación matemática: restamos 50 a cada píxel para oscurecer la foto
matriz_oscura = matriz_píxeles - 50
# Nos aseguramos de que los números no bajen de 0 (negro absoluto)
matriz_oscura = np.clip(matriz_oscura, 0, 255).astype(np.uint8)

# 4. Pillow toma la matriz de NumPy y la convierte de nuevo en foto
foto_final = Image.fromarray(matriz_oscura)

# 5. Guardamos el resultado en un nuevo archivo
foto_final.save("paisaje_oscuro.jpg")
````

En conclusión, mientras que NumPy analiza las tripas numéricas de los datos, Pillow proporciona los ojos y las manos para interactuar con archivos gráficos reales en el mundo exterior.



<hr>



## ¿Qué es Matplotlib?

Matplotlib es la librería de Python más antigua, estable y utilizada para la creación de gráficos y visualizaciones de datos. En el ecosistema de la programación, si NumPy es el cerebro matemático que calcula millones de datos y Pillow es el estudio fotográfico, Matplotlib es el lienzo de dibujo y la imprenta técnica que convierte esos fríos números en gráficos de barras, diagramas de dispersión, mapas de calor o líneas de tendencia.
Fue creada en 2003 por John Hunter con un objetivo claro: querían que Python tuviera un sistema de gráficos similar al de MATLAB (un software científico muy caro), pero de código abierto y completamente gratuito para todo el mundo.

### La conexión perfecta: ¿Por qué Matplotlib y NumPy son inseparables?

Si intentas usar Matplotlib de forma aislada, te darás cuenta de que le falta potencia. Su verdadera fuerza despierta cuando trabaja en equipo con NumPy debido a un flujo de trabajo muy natural:
1. NumPy genera y organiza las coordenadas: Imagina que quieres dibujar una onda matemática (como el oleaje del mar). NumPy se encarga de calcular miles de puntos exactos con las posiciones X e Y en una milésima de segundo.
2. Matplotlib dibuja la escena: Matplotlib toma esos arrays numéricos de NumPy y los interpreta como las coordenadas espaciales de un lienzo. Traza las líneas que unen los puntos, añade los ejes, los números, los títulos y las cuadrículas de fondo.
3. Optimización de memoria: Matplotlib está diseñado de forma interna para "entender" la estructura homogénea de los arrays de NumPy. Esto permite que el programa dibuje gráficos con millones de puntos de datos sin ralentizar tu ordenador.

### ¿Cómo funciona en la práctica? (La anatomía de un gráfico)

Para usar Matplotlib de forma sencilla, la comunidad siempre utiliza un módulo interno llamado pyplot (que se importa casi por ley universal con el alias plt).
Conceptualmente, Matplotlib divide sus gráficos en dos partes importantes:
* The Figure (La Figura): Es la ventana completa o la hoja de papel en blanco. Puede albergar un solo gráfico o una colección de varios gráficos pequeños puestos uno al lado del otro.
* The Axes (Los Ejes): Es el gráfico propiamente dicho. El recuadro que contiene el eje horizontal (X), el eje vertical (Y), las etiquetas, el título y los datos dibujados.

Ejemplo práctico: Cómo cooperan en el código real

Mira lo sencillo que es generar datos matemáticos con NumPy y dibujar un gráfico de líneas limpio, etiquetado y profesional usando Matplotlib:
````
import numpy as np
import matplotlib.pyplot as plt

# 1. NumPy genera los datos: 100 puntos en el eje X y sus cuadrados en el eje Y
eje_x = np.linspace(0, 10, 100)  # 100 números espaciados entre 0 y 10
eje_y = np.sin(eje_x)             # Calcula el seno matemático de cada número

# 2. Matplotlib empieza a dibujar sobre el lienzo
plt.plot(eje_x, eje_y, color="blue", linestyle="--", label="Onda Seno")

# 3. Añadimos detalles estéticos para que se entienda el gráfico
plt.title("Mi Primer Gráfico Científico")
plt.xlabel("Tiempo (segundos)")
plt.ylabel("Amplitud")
plt.grid(True)     # Añade una cuadrícula gris de fondo
plt.legend()       # Muestra la etiqueta "Onda Seno" en una esquina

# 4. Mostramos el lienzo final en la pantalla
plt.show()
````
¿Qué tipos de gráficos puede hacer?

Matplotlib es prácticamente infinito, pero sus herramientas más utilizadas son:
* plt.plot(): Gráficos de líneas (ideales para ver cómo cambia algo con el tiempo).   
* plt.bar(): Gráficos de barras (ideales para comparar categorías como ventas por mes).   
* plt.scatter(): Gráficos de dispersión o nubes de puntos (ideales para ver si dos variables se relacionan entre sí).   
* plt.hist(): Histogramas (ideales para ver cómo se distribuyen tus datos numéricos).

En conclusión, Matplotlib toma el poder numérico puro de NumPy y lo traduce en un idioma visual que cualquier ser humano puede comprender de un solo vistazo en un informe, presentación o artículo científico.   



<hr>



## ¿Qué es Pandas?

Pandas es la librería de Python más importante y utilizada para el análisis, la manipulación y la limpieza de datos. En el mundo de la tecnología, si NumPy es el motor de cálculo de alta potencia, Pandas es la hoja de cálculo de Excel inteligente dentro de tu código [Pandas, NumPy, Matplotlib, Seaborn, sklearn].
Fue creada en 2008 por Wes McKinney para solucionar una gran necesidad: la comunidad científica tenía herramientas para cálculos puros, pero los analistas de datos del mundo real necesitaban una herramienta cómoda para abrir archivos cotidianos (como .csv, hojas de Excel o tablas de bases de datos de SQL), limpiarlos cuando venían con errores y analizarlos de forma rápida.

### La conexión perfecta: ¿Por qué Pandas y NumPy son inseparables?

Muchos programadores primerizos se confunden y no saben dónde termina NumPy y dónde empieza Pandas. La realidad es que no compiten, sino que cooperan de forma jerárquica:
1. NumPy pone los cimientos de hormigón: NumPy es excelente manejando bloques puros de números (matrices), pero tiene un problema: no sabe trabajar bien si mezclas texto con números en la misma tabla, y no te permite ponerle "nombres" a las columnas para saber qué significan.
2. Pandas construye el edificio encima: Pandas toma las matrices ultra rápidas de NumPy y les añade un "envoltorio" amigable. Te permite poner etiquetas con nombres a las columnas (como "Precio", "Fecha" o "Nombre del Cliente"), manejar texto sin problemas y gestionar filas enteras de información.
3. El rendimiento oculto: Cuando le pides a Pandas que calcule el promedio de una columna con 50 millones de clientes, Pandas no va fila por fila de forma lenta; por debajo, le pasa esa columna a NumPy para que realice el cálculo en una milésima de segundo a nivel de procesador.

### ¿Cómo funciona en la práctica? (Las 2 Estructuras Clave)

Para dominar Pandas solo necesitas entender los dos objetos en los que organiza la información:

1. La Serie (Series)

Es el equivalente a una sola columna de datos. Imagina una lista que contiene las edades de 5 personas. Es una estructura de una sola dimensión, pero a diferencia de una lista normal de Python, cada posición tiene un nombre o índice (por ejemplo, saber que la fila 0 pertenece a "Ana" y la fila 1 a "Carlos").

2. El DataFrame

Es la estrella de la librería. Es la tabla completa, compuesta por muchas Series (columnas) una al lado de la otra. Tiene un eje de filas (índices numéricos o fechas) y un eje de columnas con nombres de texto. Es exactamente la cuadrícula visual que ves cuando abres una hoja de Excel.

Ejemplo práctico: Cómo cooperan en el código real

Mira lo intuitivo que es crear datos estructurados y analizarlos en Pandas apoyándonos en el motor numérico subyacente:
````
import numpy as np
import pandas as pd

# 1. Creamos un diccionario con datos de una tienda
# Mezclamos texto, números enteros y números aleatorios generados con NumPy
datos_tienda = {
    "Producto": ["Zapatos", "Camisa", "Pantalón", "Chaqueta"],
    "Categoría": ["Moda", "Moda", "Moda", "Moda"],
    "Precio_Base":,
    "Unidades_Vendidas": np.random.randint(10, 50, size=4) # NumPy genera las ventas aleatorias
}

# 2. Convertimos el diccionario en un DataFrame de Pandas (Nuestra "Hoja de Excel")
df = pd.DataFrame(datos_tienda)

# 3. Pandas nos permite calcular columnas nuevas de forma masiva (gracias a NumPy)
df["Ingresos_Totales"] = df["Precio_Base"] * df["Unidades_Vendidas"]

print("--- Nuestra Tabla de Datos ---")
print(df)

print("\n--- Resumen Estadístico Rápido ---")
# .describe() nos da medias, mínimos, máximos y desviaciones calculadas en un segundo
print(df["Ingresos_Totales"].describe())
````
Las herramientas más utilizadas de Pandas:

* pd.read_csv() / pd.read_excel(): Abren archivos externos gigantescos en una sola línea de código.
* df.dropna() / df.fillna(): Encuentran y eliminan (o rellenan) las casillas vacías o con errores en la tabla.
* df.groupby(): Agrupan los datos por categorías (por ejemplo, agrupar las ventas por "País" o por "Mes") para sacar resúmenes automáticos.

En conclusión, Pandas humaniza el poder matemático de NumPy, dándote una interfaz cómoda, estructurada y lógica para limpiar y exprimir el valor de cualquier base de datos por compleja que sea.



<hr>



## ¿Qué es Seaborn?

Seaborn es una librería de Python especializada en la creación de gráficos estadísticos atractivos, modernos y listos para su publicación. Si Matplotlib es el lienzo en blanco y los pinceles básicos, Seaborn es el diseñador gráfico experto que automatiza el dibujo para que consigas visualizaciones espectaculares con poquísimo esfuerzo.
Fue creada en 2014 por Michael Waskom para solucionar dos problemas recurrentes de Matplotlib: lo difícil que resultaba hacer que los gráficos se vieran bonitos de forma predeterminada y lo complejo que era representar relaciones estadísticas avanzadas sin picar decenas de líneas de código.

### La conexión perfecta: ¿Por qué Seaborn, Pandas y NumPy trabajan juntos?

En el análisis de datos, estas tres librerías forman una pirámide perfecta donde cada una cumple un rol esencial:
1. NumPy pone el poder del procesador: Realiza los cálculos matemáticos pesados en milisegundos (medias, desviaciones, nubes de puntos).
2. Pandas estructura la información: Organiza los datos en una tabla ordenada con filas y nombres de columnas (DataFrames).
3. Seaborn lee a ambas y las dibuja: Está diseñado para entender de forma nativa las tablas de Pandas y los arrays de NumPy. Solo tienes que decirle a Seaborn: "Usa esta tabla y cruza la columna Edad con la columna Salario". De manera interna, Seaborn extraerá los números a través de NumPy, calculará las tendencias estadísticas y pintará el gráfico con una paleta de colores profesional.

### ¿Cómo funciona en la práctica? (Sus 3 pilares mágicos)

* Estética automatizada (sns.set_theme): Al activar Seaborn, se eliminan los bordes toscos y los colores chillones de Matplotlib por defecto. Los sustituye por fondos grises o blancos muy limpios, cuadrículas sutiles y paletas de colores diseñadas para que los daltónicos puedan interpretarlas correctamente.
* Mapeo semántico (El argumento hue): Es una de sus mejores funciones. Si tienes un gráfico de puntos de "Peso" vs "Altura", puedes añadir el argumento hue="Género". Al hacerlo, Seaborn dividirá los puntos automáticamente en dos colores distintos según el género y creará una leyenda explicativa sin que tú tengas que programar nada más.
* Estadística visual integrada: Muchos gráficos de Seaborn calculan de forma oculta intervalos de confianza, líneas de regresión (tendencias) o curvas de densidad de probabilidad, dibujándolas directamente sobre la pantalla.

Ejemplo práctico: Cómo cooperan en el código real

Mira lo sencillo que es cargar una tabla de datos (un DataFrame de Pandas alimentado por NumPy) y crear un gráfico avanzado de dispersión con línea de tendencia matemática integrada:
````
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 1. Activamos el diseño estético de Seaborn por defecto
sns.set_theme(style="darkgrid")

# 2. NumPy genera datos simulados para una consulta médica
edades = np.random.randint(18, 80, size=100)
presion_arterial = edades * 1.5 + np.random.normal(0, 10, size=100) # Relación matemática
fumador = np.random.choice(["Sí", "No"], size=100)

# 3. Pandas los organiza en una cómoda tabla
datos_medicos = pd.DataFrame({
    "Edad": edades,
    "Presión": presion_arterial,
    "Fumador": fumador
})

# 4. Seaborn dibuja una relación estadística compleja en una sola línea
# Hace un gráfico de puntos, los pinta por color según si fuman y traza la tendencia
sns.lmplot(x="Edad", y="Presión", hue="Fumador", data=datos_medicos)

# 5. Mostramos el resultado usando el motor de Matplotlib
plt.show()
````
Gráficos estrella de Seaborn que debes conocer:

* sns.heatmap(): El famoso Mapa de Calor. Convierte una tabla de números en una cuadrícula de colores (los números altos brillan y los bajos se oscurecen). Es el rey para ver qué variables están correlacionadas.
* sns.boxplot(): Diagramas de caja. Ideal para ver resúmenes estadísticos (promedios, máximos y mínimos) de varias categorías lado a lado.
* sns.pairplot(): Hace una matriz de gráficos. Si le pasas una tabla con 5 columnas, te dibuja de golpe un mapa de cuadrículas cruzando todas las columnas entre sí para que descubras patrones ocultos al instante.

En conclusión, Seaborn es la herramienta que convierte los datos crudos de NumPy y Pandas en historias visuales atractivas, permitiendo que cualquier analista descubra tendencias y presente sus conclusiones de una forma clara y profesional.



<hr>



## ¿Qué es Pyplot?

Pyplot es un módulo interno de la librería Matplotlib que funciona como una "consola de mandos" simplificada para dibujar gráficos en Python. Si Matplotlib es una gigantesca fábrica de herramientas visuales, Pyplot es el interruptor principal que te permite pintar líneas, barras o puntos en la pantalla utilizando comandos muy cortos, directos y secuenciales.
Casi nunca verás escrito import matplotlib; la convención o norma universal en el mundo de la programación es importar directamente este módulo bajo el alias plt mediante la frase:
````
import matplotlib.pyplot as plt.
````

### La conexión perfecta: ¿Por qué Pyplot y NumPy trabajan juntos?

En la ciencia de datos, NumPy es el cerebro matemático y Pyplot es el brazo con el pincel. Su relación se basa en un flujo de trabajo lógico y ultra rápido:
1. NumPy fabrica las coordenadas: Si quieres dibujar una curva, una trayectoria o una distribución de datos, NumPy calcula los miles de puntos numéricos necesarios (las posiciones de los ejes X e Y) en una milésima de segundo.
2. Pyplot lee los bloques de NumPy: Pyplot está programado para entender perfectamente los arrays de NumPy. No necesitas decirle que recorra los números uno a uno; simplemente le pasas el bloque y Pyplot sabe exactamente dónde ubicar cada punto en el lienzo.
3. Pintado secuencial: Pyplot funciona como un "historial de capas". Cada comando que escribes añade un elemento nuevo (una línea, un título, una cuadrícula) sobre el mismo lienzo antes de mostrar el resultado final.

### ¿Cómo funciona en la práctica? (El concepto de "Lienzo Actual")

Para entender Pyplot de forma sencilla, imagina que tienes un pintor frente a un caballete. Cada línea de código es una orden directa para ese pintor:
• plt.figure(): "Pon un lienzo en blanco sobre el caballete".
• plt.plot(x, y): "Toma las coordenadas X e Y de NumPy y traza una línea azul que las una".
• plt.title("Mi gráfico"): "Escribe este título con letras grandes en la parte de arriba".
• plt.show(): "Da un paso atrás y muéstrale el cuadro terminado al mundo". (Este comando abre la ventana visual en tu ordenador).

Ejemplo práctico: Cómo cooperan en el código real

Mira lo intuitivo que es generar una función matemática con NumPy y dibujarla paso a paso usando las capas de Pyplot:
````
import numpy as np
import matplotlib.pyplot as plt

# 1. NumPy calcula los números (100 puntos espaciados entre 0 y 20)
x = np.linspace(0, 20, 100)
y = np.sqrt(x)  # Calcula la raíz cuadrada de cada número de golpe

# 2. Pyplot empieza a añadir capas al gráfico secuencialmente
plt.plot(x, y, color="green", linewidth=2, label="Crecimiento") # Capa 1: La línea

plt.title("Gráfico de Raíz Cuadrada con Pyplot")                 # Capa 2: El título
plt.xlabel("Eje X (Valores de entrada)")                         # Capa 3: Etiqueta horizontal
plt.ylabel("Eje Y (Resultado)")                                 # Capa 4: Etiqueta vertical
plt.grid(True)                                                  # Capa 5: Una cuadrícula de fondo
plt.legend()                                                    # Capa 6: El cuadro de leyenda

# 3. Ordenamos a Pyplot que abra la ventana y renderice el dibujo
plt.show()
````

Los comandos más importantes de Pyplot que debes conocer:

* Para el tipo de gráfico:
	* plt.plot(): Dibuja gráficos de líneas continuas (tendencias).
	* plt.scatter(): Dibuja nubes de puntos sueltos (dispersión).
	* plt.bar(): Crea diagramas de barras verticales.
	* plt.hist(): Construye histogramas automáticos para ver distribuciones.
* Para adornar y etiquetar:
	* plt.xlim() / plt.ylim(): Configuran los límites mínimos y máximos de los ejes (por ejemplo, forzar a que el gráfico empiece estrictamente en el número 0).
	* plt.savefig("mi_grafico.png"): Guarda el lienzo actual en un archivo de imagen en tu ordenador sin necesidad de abrir la ventana interactiva.

En conclusión, Pyplot es la interfaz amigable que vuelve sencillo lo complejo, permitiendo que interactúes con la enorme maquinaria gráfica de Matplotlib mediante instrucciones cortas, lógicas y estructuradas sobre tus datos de NumPy.



<hr>


