Clustering con incertidumbre para anillos con ruido

El código está estructurado de manera que al principio se hace toda la implementación de los métodos que usará el algoritmo. Después de la implementación de cada
método hay una pequeña prueba para comprobar que ese segmento de código funciona como se espera. 
Tras la implementación se encuentra la parte de experimentación, donde se han generado archivos .csv de puntos que forman circunferencias y posteriormente se experimenta
con ellos.

Para hacer un experimento, es importante cargar todas las celdas hasta que acabe la parte de implementación. Será necesario tener un archivo .csv que contenga los puntos
en formato de dos columnas, una para x, otra para y, que representarían las coordenadas de los puntos. Ofrecemos unos métodos para la generación de puntos aleatorios en una
circunferencia dada (fijando su centro y radio) y también un escritor de .csv, para hacer que los datos persistan.

Para la generación de puntos y posterior escritura en un fichero .csv, habrá que llamar a genera_puntos_circulo(centro, radio, n), donde centro es una tupla con las coordenadas
del centro del círculo (x, y), radio es el radio del círculo y n es el número de puntos a generar. Esto generará una lista de puntos que puede concatenarse con otras listas de 
puntos de otros círculos, pudiendo así generar puntos de tantos círculos como se quiera. Ejemplo:

circulo1 = genera_puntos_circulo((6, 12), 2, 30)
circulo2 = genera_puntos_circulo((10, 10), 1, 20)
circulo3 = genera_puntos_circulo((12, 6), 2.5, 30)
circulo4 = genera_puntos_circulo((3, 6), 2, 30)
puntos_circulos = circulo1+circulo2+circulo3+circulo4

Para escribirlo en un fichero .csv siguiendo el formato utilizado, simplemente habría que llamar a la función escribe_csv(puntos_circulos, nombre_csv), donde se pasan como 
parámetros una lista de puntos (en este caso, los que hemos generado formando círculos) y el nombre del fichero .csv. Ejemplo:
escribe_csv(puntos_circulos, "Puntos5.csv")

Esto generará un .csv en la carpeta donde esté el Notebook, lugar en el cual también podríamos introducir un fichero no generado mediante este código para usarlo.

Una vez cumplidos estos requisitos, podremos realizar un experimento utilizando la función evalua(csv, clusters_reales, n_busquedas, iteraciones_por_busqueda, 
metodo_clusters_iniciales, n_clusters, margen_error, mostrar_res_individuales), para la cual es necesario conocer los clusters correctos, es decir, las circunferencias
que deberían encontrarse utilizando el algoritmo. 
	
	1. "csv" es el nombre del fichero .csv del que se tomarán los puntos
	2. "clusters_reales" es una lista de tuplas que representan los círculos que deberían encontrarse
	3. "n_busquedas" se refiere al número de veces que se repetirá el experimento, dado que hay un componente aleatorio importante
	    en el algoritmo. 
	4. "iteraciones_por_busqueda" se refiere al número de iteraciones que realizará el algoritmo antes de parar. "metodo_clusters_iniciales" se refiere al método
	    de búsqueda de clusters iniciales seleccionado, acepta los valores: "estandar", "random", "cercania", "bordes" y "dos_puntos"; cada uno refiriéndose a uno de los métodos
	    desarrollados para la búsqueda de los mismos. "estandar" seleccionará el último método desarrollado, "random" seleccionará el método aleatorio, "bordes" seleccionará el
	    método aleatorio que tiene en cuenta los bordes de la lista de puntos, "cercania" seleccionará el método que busca 3 puntos cercanos entre sí. "dos_puntos" seleccionará
	    el método que escoge dos puntos aleatorios y genera un círculo con ellos.
	5. "n_clusters" selecciona el número de clusters iniciales a generar
	6. "margen_error" escoge el margen de error que está permitido entre la solución encontrada y la solución real
	7. "mostrar_res_individuales" si es True, muestra los valores encontrados en cada búsqueda y su evaluación

Un ejemplo de uso de este código para realizar un experimento sería:

clusters_reales = [((9, 5), 2), ((9, 5), 3), ((20, 18), 6)]
evalua('Puntos2.csv', clusters_reales, 50, 20, "estandar", 3, 0.2, False)

"clusters_reales" es un ejemplo de lista de circunferencias en el formato que se sigue para el correcto funcionamiento de evalua()