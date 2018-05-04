<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Ejercitación

## Funciones

Definir las siguientes funciones numéricas
1. `prom3` que recibe tres números y devuelve su promedio.  
  P.ej. `prom3(1,2,4)` debe evaluar a `2.3333333333` aprox..

1. `estanOrdenados` que recibe tres números, y devuelve `True` si están ordenados de menor a mayor, o `False` en caso contrario.  
  P.ej. `estanOrdenados(1,2,4)` y `estanOrdenados(11,2,4)` deben evaluar a `True` y `False` respectivamente.  
  Ayuda: se pueden usar las palabras `and` y `or` para conectar condiciones. P.ej. `4 < 5 or 12 < 8` y `4 < 5 and 12 < 8` evalúan a `True` y `False` respectivamente, porque una de las dos condiciones se verifica, pero no las dos.

1. `elevarALaSuma` que recibe tres números, y debe devolver el resultado de elevar al primero a la potencia equivalente a la suma de los otros dos.  
Dicho de otra forma, si llamamos a los parámetros `a,b,c`, debe devolver el resultado de elevar `a` a la potencia `b+c`.
    P.ej. `elevarALaSuma(2,3,5)` debe evaluar a 256, que es 2 a la octava.  
    Recordar que `**` denota "elevar a" en Python, p.ej. `2**5` evalúa en 32.

1. `minPotencia`, que recibe tres números, y debe devolver el resultado de elevar al primero a una potencia equivalente al *mínimo* entre los otros dos.  
    P.ej. tanto `minPotencia(2,3,5)` como `minPotencia(2,5,3)` deben evaluar a 8, que es 2 al cubo, dado que el mínimo entre 3 y 5 es 3.

1. `porElPromedio`, recibe cuatro números, devuelve el primero multiplicado por el promedio de los otros tres.  
P.ej. `porElPromedio(3,1,2,4)` debe evaluar a 7, dado que el promedio entre 1, 2 y 4 es 7/3.

1. `dobleOTriple`, recibe dos números. Si el primero es positivo (incluyendo 0), debe devolver el *doble* del segundo. Caso contrario, debe devolver el *triple* del segundo.  
P.ej. `dobleOTriple(3,4)` y `dobleOTriple(-3,4)` deben evaluar a 8 y 12 respectivamente.

<br/>

## Listas - operaciones básicas
Definir las siguientes funciones que involucran listas de números.

1. `productoPrimerosDos`, recibe una lista, devuelve el producto de sus primeros dos elementos.  
P.ej. `productoPrimerosDos([3, 8, 21, 94, 9, 41])` debe evaluar a 24.

1. `productoUltimosDos`, recibe una lista, devuelve el producto de sus *últimos* dos elementos.  
P.ej. `productoUltimosDos([3, 8, 21, 94, 9, 41])` debe evaluar a 369 (41 * 9).  
Ayuda: recordar que se pueden usar índices negativos.

1. `sumaDosElems`, recibe una lista y dos índices, devuelve la suma de los elementos de la lista en esos índices.  
P.ej. `sumaDosElems([3, 8, 21, 94, 9, 41], 2, 4)` debe evaluar a 30, porque los elementos en posiciones 2 y 4 de la lista son 21 y 9 respectivamente (recordar que el índice del primer elemento es 0).

1. `estanAmbos`, recibe una lista y dos números. Devuelve `True` si los dos números están en la lista, `False` en caso contrario.  
P.ej. `estanAmbos([3, 8, 21, 94, 9, 41], 94, 8)` y `estanAmbos([3, 8, 21, 94, 9, 41], 94, 16)` deben evaluar a `True` y `False` respectivamente.
Ayuda: usar `in`, y lo que se habló en un ejercicio anterior sobre `and` y `or`.

1. `estaAntes`, recibe una lista y dos números. Devuelve `True` si el primer número aparece antes en la lista que el segundo. Se puede suponer que los dos números están en la lista.  
P.ej. `estaAntes([3, 8, 21, 94, 9, 41], 8, 94)` y `estaAntes([3, 8, 21, 94, 9, 41], 94, 8)` deben evaluar a `True` y `False` respectivamente.

1. Modificar `estaAntes`, para que devuelva `False` si no se verifica que los dos números están en la lista.

1. `promLista`, recibe una lista y devuelve su promedio.  
Ayuda: usar `sum` y `len`.

1. `rango`, que devuelve el rango de una lista, definido como la diferencia entre sus valores máximo y mínimo.  
P.ej. `rango([3, 8, 21, 94, 9, 41])` debe evaluar a 91 (94 - 3).  
Ayuda: recordar las funciones `max` y `min`.

1. `valoresExtremos`, recibe una lista, devuelve una lista de dos elementos, los valores máximos y mínimos de esa lista.  
P.ej. `rango([3, 8, 21, 94, 9, 41])` debe evaluar a `[94,3]`.

<br/>

## Listas - recorridos
Definir las siguientes funciones que involucran listas de números.
Se sugiere hacer dos implementaciones, una usando `for` y otra con list comprehensions, al menos para las funciones `dobles`, `multiplos`, `enAbsoluto` y `elementosEntre`. Para las primeras dos, se sugiere hacer una tercer implementación que use `map` o `filter`.

1. `dobles`, recibe una lista, devuelve la lista formada por el doble de cada elemento.  
P.ej. `dobles([3, 8, 21, 94, 9, 41])` debe evaluar a `[6, 16, 42, 188, 18, 82]`.

1. `todosAlCuadrado`, recibe una lista, devuelve la lista formada por cada elemento elevado al cuadrado.  
P.ej. `todosAlCuadrado([3, 8, 21, 94, 9, 41])` debe evaluar a `[9, 64, 441, 8836, 81, 1681]`.

1. `doblesSinElPrimero`, recibe una lista, devuelve la lista formada por el doble de cada elemento, *excepto el primero*.  
P.ej. `doblesSinElPrimero([3, 8, 21, 94, 9, 41])` debe evaluar a `[16, 42, 188, 18, 82]`.  
Ayuda: usar la notación `[1:]`.

1. `porElPrimero`, recibe una lista, devuelve la lista formada por el resultado de multiplicar el primer elemento por cada uno de los otros.  
P.ej. `porElPrimero([3, 8, 21, 94, 9, 41])` debe evaluar a `[24, 63, 282, 27, 123]`.

1. `triplesOCuadruples`, recibe una lista, devuelve la lista formada por el triple o el cuádruple de cada elemento salvo el primero, de acuerdo a si el primer elemento es positivo o negativo respectivamente.  
P.ej. `triplesOCuadruples([3, 8, 21, 94, 9, 41])` y `initialex.triplesOCuadruples([-3, 8, 21, 94, 9, 41])` deben evaluar a `[24, 63, 282, 27, 123]` y `[32, 84, 376, 36, 164]` respectivamente.

1. `multiplos(list,n)` devuelve la lista de los elementos de `list` que sean múltiplos de `n`.  
P.ej. `multiplos([3, 8, 21, 94, 9, 41], 3)` debe evaluar a `[3, 21, 9]`.

1. `restos(list,n)` devuelve la lista formada por el *resto* de dividir cada elmento de `list` por `n`.
P.ej. `restos([3, 8, 21, 94, 9, 41], 3)` debe evaluar a `[0,2,0,1,0,2]`.

1. `restosSignificativos(list,n)`, devuelve la lista formada por el *resto* de dividir cada elmento de `list` por `n`, considerando solamente los elementos que no son múltiplos de `n`.
P.ej. `restosSignificativos([3, 8, 21, 94, 9, 41], 3)` debe evaluar a `[2,1,2]`.

1. `multiplosDividido(list,n)` devuelve la lista de dividir por `n`, cada elemento de `list` que es múltiplo de `n`.  
P.ej. `multiplosDividido([3, 8, 21, 94, 9, 41], 3)` debe evaluar a `[1,7,3]`.

1. `enAbsoluto(list)` devuelve la lista conformada por el valor absoluto (función `abs`) de cada elemento de `list`.  
P.ej. `enAbsoluto([3, -8, 21, 94, 9, -41])` debe evaluar a `[3, 8, 21, 94, 9, 41]`.

1. `positivosAlDoble(list)`, devuelve la lista conformada por el doble de cada elemento positivo de `list`.  
P.ej. `positivosAlDoble([3, -8, 21, 94, 9, -41])` debe evaluar a `[6,42,188,18]`.

1. `elementosEntre(list,min,max)`, la lista conformada por los elementos de `list` cuyo valor esté entre `min` y `max`.  
P.ej. `elementosEntre([3, 8, 21, 94, 9, 41], 10, 50)` debe evaluar a `[21,41]`.

<br/>

## Listas - un poco más complejos
1. `sinElMaximo(list)`, devuelve la lista conformada por todos los elementos de `list` salvo el máximo.  
P.ej. `sinElMaximo([3, 8, 21, 94, 9, 41])` debe evaluar a `[3, 8, 21, 9, 41]`.

1. `sinValoresExtremos(list)`, devuelve la lista conformada por todos los elementos de `list` salvo el mínimo y el máximo.

1. `llevandoTodosAlMenosA(list,n)`, devuelve la lista producto de reemplazar en `list` cada elemento menor a `n`, por `n`. La lista `list` no debe modificarse.  
P.ej. `llevandoTodosAlMenosA([3, 8, 21, 94, 9, 41],10)` debe evaluar a `[10, 10, 21, 94, 10, 41]`.

1. `agregandoPares(list1,list2)`, devuelve el resultado de concatenar a `list1`, los elementos pares de `list2`. No deben modificarse ni `list1` ni `list2`.  
P.ej. `agregandoPares([3,8,21,94,9,41],[11,12,17,21,4])` debe evaluar a `[3,8,21,94,9,41,12,4]`: todos los de `list1`, seguidos por los pares en `list2`.  
Se puede usar la función `multiplos` definida en un punto anterior.

1. `desviaciones(list)`, devuelve la lista formada por la desviación (en valor absoluto) de cada elemento de `list` respecto de su promedio.  
P.ej. `initialex.desviaciones([7,8,3,5,2])` debe evaluar a `[2.0, 3.0, 2.0, 0.0, 3.0]`.  
Se puede usar la función `promLista` definida en un punto anterior.

1. `desviacionMedia(list)`, devuelve la desviación media de la lista (o sea, el promedio de las desviaciones de cada elemento).  
P.ej. `desviacionMedia([7,8,3,5,2])` debe evaluar a `2.0`.


<br/>

## Para investigar otros temas
Se presentan algunas funciones para cuya resolución pueden servir algunas herramientas que no vimos en la reunión del miércoles 2 de mayo, para los curiosos.

1. `productoPuntual`, recibe dos listas (o iteradores) de la misma longitud, devuelve la lista formada por el producto de los elementos correspondientes por posición.  
P.ej. `productoPuntual([3,8,21,94,9,41], [2,3,1,4,2,3])` debe evaluar a `[6, 24, 21, 376, 18, 123]`.  
Se puede resolver en una línea, usando la función `zip` y una list comprehension.

2. `productoProgresivo`, recibe una lista, devuelve el resultado de multiplicar el primer elemento por 1, el segundo por 2, el tercero por 3 y así siguiendo.  
P.ej. `productoProgresivo([3,8,21,94,9,41])` debe evaluar a `[3, 16, 63, 376, 45, 246]`.  
Se puede resolver en una línea, usando el punto anterior y `range`.

1. `esListaOrdenada(list)`: debe devolver `True` si los elementos de `list` están ordenados de menor a mayor, y `False` en caso contrario.  
Se puede resolver en una línea. En mi resolución, armé la de los pares de elementos consecutivos de `list` usando `zip`, y usé la función `all` para la evaluación.

1. `puntosEntre(inicio,fin)`: `inicio` y `fin` son dos pares ordenados, devuelve la lista (o iterador) de puntos de coordenadas enteras que entran en el cuadrado delimitado por estos dos puntos.  
P.ej. `puntosEntre((1,1),(3,4))` debe evaluar a la lista `[(1, 1), (1, 2), (1, 3), (1, 4), (2, 1), (2, 2), (2, 3), (2, 4), (3, 1), (3, 2), (3, 3), (3, 4)]`, o a un generador de dicha lista.  
En mi resolución, usé una list comprehension con dos `for` que arma un producto cartesiano.

1. `esReordenamientoDe(list1,list2)`, indica si `list2` tiene los mismos elementos de `list1`, tal vez en distinto orden. En realidad los "list" pueden ser también generadores.  
P.ej. `initialex.esReordenamientoDe([1,3,5,2,0,4], range(6))` debe evaluar a `True`.  
De este propongo dos resoluciones: una que aprovecha la función `set`, otra que usa la función `all`.

 