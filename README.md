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
* plt.figure(): "Pon un lienzo en blanco sobre el caballete".
* plt.plot(x, y): "Toma las coordenadas X e Y de NumPy y traza una línea azul que las una".
* plt.title("Mi gráfico"): "Escribe este título con letras grandes en la parte de arriba".
* plt.show(): "Da un paso atrás y muéstrale el cuadro terminado al mundo". (Este comando abre la ventana visual en tu ordenador).

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
* Eliminar las filas con nulos (dropna): Borra cualquier fila que contenga al menos un valor vacío.python
df_limpio = df.dropna()

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
Clase de Tipo	        	Conversión al almacenar un NA	Valor Centinela NA
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
