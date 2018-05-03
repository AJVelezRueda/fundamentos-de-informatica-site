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

<!--
    def prom3(n1, n2, n3):
    return (n1 + n2 + n3) / 3

def estanOrdenados(n1, n2, n3):
    return n1 <= n2 and n2 <= n3

def elevarALaSuma(n,p1,p2):
    return n**(p1+p2)

def minPotencia(n,p1,p2):
    return n**(min(p1,p2))

def porElPromedio(n,m1,m2,m3):
    return n*(prom3(m1,m2,m3))

def dobleOTriple(n,s):
    if (s >= 0):
        return n * 2
    else:
        return n * 3

def sumaDosElems(list, index1, index2):
    return list[index1] + list[index2]

def promLista(list):
    return sum(list) / len(list)

def dobles(list):
    return [n * 2 for n in list]

def todosAlCuadrado(list):
    return [n**2 for n in list]

def doblesSinElPrimero(list):
    return dobles(list)[1:]

def porElPrimero(list):
    return [n * list[0] for n in list[1:]]

def doblesOTriples(list):
    if (list[0] >= 0):
        return doblesSinElPrimero(list)
    else:
        return [n * 3 for n in list[1:]]
    
def multiplos(list, n):
    return [x for x in list if x % n == 0]

def restos(list, n):
    return [x % n for x in list]

def enAbsoluto(list):
    return [abs(x) for x in list]

def elementosEntre(list,min,max):
    return [x for x in list if x >= min and x <= max ]

def rango(list):
    return max(list) - min(list)

def valoresExtremos(list):
    return [max(list), min(list)]

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

