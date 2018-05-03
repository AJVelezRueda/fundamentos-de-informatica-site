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
P.ej. `productoPrimerosDos([3, 8, 21, 94, 9, 41])` debe evaluar a 369 (41 * 9).  
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

1.




<!--
def elementosEntre(list,min,max):
    return [x for x in list if x >= min and x <= max ]

def sinElMaximo(list):
    return [x for x in list if x < max(list)]

def sinValoresExtremos(list):
    return [x for x in list if x not in valoresExtremos(list)]

def llevandoTodosAlMenosA(list,n):
    return [max(n,x) for x in list]

def agregandoPares(list1, list2):
    return list1 + multiplos(list2, 2)

def desviaciones(list):
    return [abs(x - promLista(list)) for x in list]

def desviacionMedia(list):
    return promLista(desviaciones(list))

def productoPuntual(list1,list2):
    return [n * m for n,m in zip(list1,list2)]

def productoProgresivo(list):
    return productoPuntual(list, (x+1 for x in range(len(list))))

def esListaOrdenada(list):
    return all(n1 < n2 for (n1,n2) in zip(list, list[1:]))

def puntosEntre(inicio,fin):
    ix, iy = inicio
    fx, fy = fin
    return ((x,y) for x in range(ix, fx+1) for y in range(iy, fy+1))

-->

