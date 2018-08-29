# Pauta correci�n  Control 1 IIC2233-2018-2 

## 1. Verdadero y Falso (1,5 puntos)
1. En Python, las tuplas suelen almacenar datos heterog�neos.
	
	**Respuesta**: **Verdadero**.	 
2. La respuesta de `reduce(lambda x, y: (x + y) / 2, [1, 1, 3, 6])`  es 5.5.
	
	**Respuesta**: **Falso**, el resultado es 4.0 (puede ser escrito como **int** o **float**).
3. Un *deque* sirve para simular un *stack* y una cola, al mismo tiempo.
	
	**Respuesta**: **Verdadero**.

4. Los diccionarios son eficientes para revisar si un elemento est� entre los valores.
	
	**Respuesta**: **Falso**, es eficiente s�lo para verificar las llaves. 
6. Asumiendo que dicci es un diccionario, la expresi�n *'foo' in dicci* devolver� _True_ si 'foo' se encuentra entre las llaves de dicci, o bien, entre sus valores.
	
	**Respuesta**: **Falso**, la expresi�n devuelve _True_ si y s�lo si est� entre las llaves. Los valores no tienen ninguna incidencia.
## Distribuci�n de puntaje
* 0.3 ptos por cada aseveraci�n correcta.
* Si la aserveraci�n es **falsa** el puntaje se distribuye de la siguiente manera:
	* 0.1 puntos si no est� justificada.
	* 0.2 puntos  si est� justificada pero no correcta completamente.
	*  0.3 puntos si est� justificada correctamente.
## 2. Sobre la actividad AC02 (1,5 puntos)
1. Explique el prop�sito de la funci�n *foreach* de la actividad.

	**Respuesta**: la funci�n `foreach(funci�n, iterable)` aplicaba una *funci�n* a cada elemento del *iterable*.
3. Escriba una funci�n llamada *print_each* que, dado un iterable, imprima sus elementos usando el foreach visto en la actividad.
	
	**Respuesta**: 
	
	**Opci�n 1**: utilizando directamente la funci�n print en *foreach*
		
	
		def print_each(iterable): 
		    foreach(print, iterable)
		
	**Opci�n 2**: utilizando una funci�n *lambda*  para realizar *print* sobre cada elemento del iterable.
	
		def print_each(iterable): 
		    foreach(lambda x: print(x), iterable)
		  
	**Respuesta alternativa**: aparte de las dos opciones entregadas, si se entregaba una funci�n que realizara el *print* solicitado, la respuesta tambi�n est� correcta. 

4. Suponga que *paises* es un iterable que contiene objetos con los atributos **sigla** y **nombre**. Escriba una funci�n que reciba dos argumentos: un iterable de pa�ses y un nombre de un pa�s. Esta funci�n deber� retornar un generador que contenga �nicamente la sigla de todos los pa�ses que calzan con ese nombre.

	**Respuesta**:
	
	**Opci�n 1**: una forma de hacerlo era por medio de un generador por comprensi�n:
	
		def siglas_de_pais(nombre_pais, paises): 
		    return (p.sigla for p in paises if p.nombre == nombre_pais)
		
	**Opci�n 2**: otra forma posible era utilizando un *map* y un *filter*:
	
		def siglas_de_pais(nombre_pais, paises): 
		    return map(lambda p1: p1.sigla, filter(lambda p2: p2.nombre == nombre_pais, paises))
	**Respuesta alternativa**: aparte de las dos opciones entregadas, si se entregaba una funci�n que retornara el generador pedido, la respuesta tambi�n est� correcta.
##  Distribuci�n de puntaje
* 0.5 puntos por cada pregunta.
##  3. Desarrollo r�pido (1 punto)

1. �Para qu� sirve el *statement* `yield`en Python?

	**Respuesta**: para devolver un generador, a trav�s de una funci�n generadora.
		
2.  Suponga que cuenta con un generador con n�meros enteros en su interior. �Qu� ocurrir� con este generador si quisi�ramos calcular el promedio de estos n�meros?

	**Respuesta**: para calcular el promedio, es necesario conocer todos los n�meros. Por lo mismo, tendremos que agotar el generador. 
	**Respuesta alternativa**:  tambi�n se pod�a responder con alguna funci�n que permitiese calcular el promedio con uso del generador.
##  Distribuci�n de puntaje
* 0.5 puntos por cada pregunta.

## 4. Lectura de c�digo (2 puntos)

Escriba el *output* del programa. Escriba, adem�s, el valor de los iteradores instanciados(asumiendo que se transforman, por ejemplo, en una lista, en donde ser�a posible ver los elementos de los iteradores, como si se le aplicara `print(list(generador))`) como **pasos intermedios**, anres de la impresi�n del resultado. Indique a qu� paso intermedio coresponde cada secuencia de valores.
### Forma 1
	a = [3, 1, 4, 1, 5, 9, 2, 6] # pi
	b = [2, 7, 1, 8, 2, 8, 2] # e
	c = [1, 4, 1, 4, 2, 1] # ra�z de 2
	resultado = {x[1] // x[2] for x in filter(lambda x: (x[0] + 1) % 3, zip(a, b, c))}
	print(resultado)
	
#### Respuesta
**Paso 1**: la funci�n *zip* retornaba el siguiente generador:

	((3, 2, 1), (1, 7, 4), (4, 1, 1), (1, 8, 4), (5, 2, 2), (9, 8, 1))
 Debido a que *zip* forma tuplas hasta recorrer completamente el iterable con menos elementos, que en este caso ser�a la lista *c*.
 
 **Paso 2**: *filter* retornaba el siguiente generador:
		 
	((3, 2, 1), (1, 7, 4), (4, 1, 1), (1, 8, 4), (9, 8, 1))
Debido a que la condici�n del *filter* era que el sucesor del primer elemento de cada tupla **no** fuera m�ltiplo de 3. El �nico elemento del iterable que no cumpl�a con eso era `(5, 2, 2)` .

**Paso 3**: resultado final, el *set* por comprensi�n resultante deb�a era:

	{8, 2, 1}
Debido  a que *set* no admite duplicados, s�lo deb�an quedar los valores distintos despu�s de la oper�ci�n realizada sobre cada tupla.

### Forma 2
	a = [3, 1, 4, 1, 5, 9, 2, 6] # pi
	b = [2, 7, 1, 8, 2, 8, 2] # e
	c = [1, 4, 1, 4, 2, 1] # ra�z de 2
	resultado = {x[1] // x[0] for x in filter(lambda x: (x[2] + 1) % 3, zip(a, b, c))}
	print(resultado)
	
#### Respuesta
**Paso 1**: la funci�n *zip* retornaba el siguiente generador:

	((3, 2, 1), (1, 7, 4), (4, 1, 1), (1, 8, 4), (5, 2, 2), (9, 8, 1))
 Debido a que *zip* forma tuplas hasta recorrer completamente el iterable con menos elementos, que en este caso ser�a la lista *c*.
 
**Paso 2**: *filter* retornaba el siguiente generador:
		 
	((3, 2, 1), (1, 7, 4), (4, 1, 1), (1, 8, 4), (9, 8, 1))
Debido a que la condici�n del *filter* era que el sucesor del tercer elemento de cada tupla **no** fuera m�ltiplo de 3. El �nico elemento del iterable que no cumpl�a con eso era `(5, 2, 2)` .

**Paso 3**: resultado final, el *set* por comprensi�n resultante deb�a era:

	{0, 8, 7}
Debido  a que *set* no admite duplicados, s�lo deb�an quedar los valores distintos despu�s de la oper�ci�n realizada sobre cada tupla.

### Forma 3
	a = [3, 1, 4, 1, 5, 9, 2, 6] # pi
	b = [2, 7, 1, 8, 2, 8, 2] # e
	c = [1, 4, 1, 4, 2, 1] # ra�z de 2
	resultado = {x[0] // x[1] for x in filter(lambda x: (x[2] + 1) % 3, zip(a, b, c))}
	print(resultado)
	
#### Respuesta
**Paso 1**: la funci�n *zip* retornaba el siguiente generador:

	((3, 2, 1), (1, 7, 4), (4, 1, 1), (1, 8, 4), (5, 2, 2), (9, 8, 1))
 Debido a que *zip* forma tuplas hasta recorrer completamente el iterable con menos elementos, que en este caso ser�a la lista *c*.
 
 **Paso 2**: *filter* retornaba el siguiente generador:
		 
	((3, 2, 1), (1, 7, 4), (4, 1, 1), (1, 8, 4), (9, 8, 1))
Debido a que la condici�n del *filter* era que el sucesor del tercer elemento de cada tupla **no** fuera m�ltiplo de 3. El �nico elemento del iterable que no cumpl�a con eso era `(5, 2, 2)` .

**Paso 3**: resultado final, el *set* por comprensi�n resultante deb�a era:

    {0, 1, 4}
Debido  a que *set* no admite duplicados, s�lo deb�an quedar los valores distintos despu�s de la oper�ci�n realizada sobre cada tupla.


## Distribuci�n de puntaje
 * 0.5 puntos por escribir correctamente el *zip* resultante
 * 0.5 puntos por escribir correctamente el *filter* resultante.
 * 1 punto por escribir el resultado final.

