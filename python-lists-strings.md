<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Python: listas y Strings

## Listas
Conforman la estructura de más sencilla, directa y utilizada en Python.

En lo que sigue se introducen muchas operaciones que se pueden hacer sobre listas. Varias de ellas sólo se mencionan.
En [este link](https://www.programiz.com/python-programming/list) pueden encontrar más detalles. 


### Construcción y acceso a elementos
Para construir una lista, la notación más sencilla es con corchetes, p.ej.
```
>>> nums = [3,8,21,2,9,44]
```

Para acceder a un elemento o una sublista (o sea, una subsecuencia de la lista), otra vez se usan corchetes, p.ej.: `nums[3]`, `nums[1:3]`, `nums[3:]`, `nums[:3]`. Lo que queda vacío a un costado del dos-puntos indica "hasta el final" o "desde el principio".  

Recordar que Python es **base 0**.  
¿Qué quiere decir esto? Que los índices arrancan desde 0, y que esta notación es "exclusive" el último, o sea que p.ej `nums[0:3]` es `[3,8,21]`, desde el 0 al 3 excluyendo el 3. Notar que `nums[3]` es `2`, el *cuarto* elemento.    

Python también acepta *números negativos* como índices en esta notación, p.ej. `nums[-1]` es el *último* elemento.

<br/>

### Agregar y quitar elementos, concatenar

Para *agregar* elementos tenemos:
* los métodos `append` y `extend`, que agregan uno o varios elementos (`extend` recibe una lista con los elementos a agregar).
* el método `insert` que permite agregar un elemento en donde se desee.

Para *quitar* elementos tenemos:
* el comando `del` que permite eliminar uno o varios elementos, indicando los índices con la notación de corchetes que vimos para accederlos. P.ej. `del(nums, [2])` elimina el tercer (recordar "base 0") elemento.  
* el método `remove`, que permite eliminar un elemento indicando el objeto que se quiere borrar. P.ej. `nums.remove(2)` elimina el `2` que está en `nums`.

Para *concatenar* listas tenemos:
* el `+`, p.ej. `["a", "b"] + ["j", "p", "q"]`.
* el `*`, que es "producto por escalar", donde la suma es la de arriba. P.ej. `nums * 3` es `nums + nums + nums`.

<br/>

### Consultas básicas
Tenemos `len`, `index`, `count`, `max`, `min`.

También hay una notación especial: `<valor> in <lista>` que devuelve `True` o `False` según si el valor es, o no, elemento de la lista.

<br/>

### Operaciones: 'in-place' vs crear otra lista
Algunas operaciones, p.ej. `append`, `extend`, `del` o `remove`, son **in-place**. Esto quiere decir que *modifican la lista sobre la que se aplican*.

Otras operaciones, p.ej. la concatenación, `filter` y `map`, **devuelven una nueva lista**, que se crea ad-hoc.

P.ej. consideremos `nums = [3,8,21,2,9,44]`. Usando `extends` tenemos
```
>>> nums.extend([7,28])
>>> nums
[3, 8, 21, 2, 9, 44, 7, 28]
```
o sea, el `extend` no devuelve nada, y modifica la lista, que ahora tiene dos elementos más.

Partiendo del mismo `nums = [3,8,21,2,9,44]`, veamos qué pasa con la concatenación:
```
>>> nums + [7,28]
[3, 8, 21, 2, 9, 44, 7, 28]
>>> nums
[3, 8, 21, 2, 9, 44]
```
la concatenación devuelve una nueva lista (que si se quiere usar más adelante, debe asignarse p.ej. a una variable), y **no modifica** la lista `nums`.

<br/>

### Métodos vs. funciones
Entre las opciones para manipular listas, algunas son funciones y otras métodos. Las funciones se escriben ... justamente, en notación función, pasando la lista por parámetro. P.ej. 
```
len(nums)
```
Los métodos van con notación de punto, aplicados a la lista, p.ej.
```
nums.index(21)
```

La existencia de métodos está relacionada a que las listas son *objetos*, y por eso admiten que se les apliquen métodos (dicho en modo purista, que les sean enviados *mensajes*).

<br/>

### Atención: `range` no genera una lista
Al invocar a `range` lo que se obtiene **no** es una lista, sino un objeto más básico que es un iterador.  
La motivación es la eficiencia, p.ej. para que la ejecución de un loop de esta forma
```
for <variable> in range(100000): 
    <bloque>
```
no implique construir una estructura con 100000 elementos, lo que no es necesario.

Para obtener la lista correspondiente a un iterador, se usa `list`.

Ejemplo en el intérprete interactivo
```
>>> range(5)
range(0, 5)
>>> list(range(5))
[0, 1, 2, 3, 4]
```

El primero no es una lista, por eso no se muestra con notación de lista. Esto tiene la consecuencia que algunas operaciones de lista no se pueden hacer, p.ej. 
```
>>> range(5) + [11]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'range' and 'list'
>>> list(range(5)) + [11]
[0, 1, 2, 3, 4, 11]
```

<br/>

## Recorridos sobre listas
Repasamos tres alternativas.

### Repetición
La forma "clásica":
```
for <elem> in <lista>:
    <bloque>
```

Si lo que se quiere es buscar, p.ej. el primer elemento que cumpla una condición, se puede usar `break` dentro del bloque.

<br/>

### Funciones de orden superior: `map`, `filter`, `reduce`
Un ejemplo de cada una:
```
>>> import functools
>>> nums = [12,15,2,8,31]
>>> list(map(lambda x: x * 2, nums))
[24, 30, 4, 16, 62]
>>> list(filter(lambda x: x > 10, nums))
[12, 15, 31]
>>> functools.reduce(lambda suma,x: suma + x, nums, 0)
68
```

Algunos comentarios:
* Se hace el `import` para poder usar `reduce`, que está en el módulo `functools`.
* Lo que devuelven `map` y `filter` no son listas sino iteradores, por eso hay que usar `list` para convertirlos a lista. Esto permite buscar el primer elemento que cumpla una condición, p.ej. `>>> next(filter(lambda x: x > 10, nums))`, sin que nunca se arme la lista de los que cumplen, con una eficiencia similar a una repetición `for` con `break`.
* La notación `lambda` permite definir *funciones anónimas* (que no llevan nombre). Por otro lado, se pueden usar `map`, `filter` y `reduce` con funciones "normales". P.ej. 
```
>>> def doble(n):
...   return n * 2
...
>>> list(map(doble, nums))
[24, 30, 4, 16, 62]
```

<br/>

### List comprehensions y generator expressions
Son mecanismos muy versátiles. Van dos ejemplos sencillos, equivalentes a `map` y `filter`.

```
>>> [x * 2 for x in nums]
[24, 30, 4, 16, 62]
>>> [x for x in nums if x > 10]
[12, 15, 31]
```

Es muy fácil combinarlos
```
>>> [x * 2 for x in nums if x > 10]
[24, 30, 62]
```

El operador ternario me da flexibilidad, p.ej. los menores a 10 al doble y el resto al triple
```
>>> [x * 2 if x < 10 else x * 3 for x in nums]
[36, 45, 4, 16, 93]
```

Esta notación admite más variables, se puede ver [la página al respecto en el tutorial oficial de Python](https://docs.python.org/3/tutorial/datastructures.html).

<br/>

Si en lugar de corchetes (list comprehension) ponemos paréntesis (generator expression), lo que obtenemos es un iterador, similar a lo que nos dan `map` o `filter`. Por eso, para obtener el primero que cumpla una condición conviene paréntesis:
```
>>> next(x for x in nums if x > 10)
12
```
por la misma cuestión de eficiencia que contamos sobre el `range`.  

Insistimos en que lo que se obtiene **no** es una lista:
```
>>> (x for x in nums if x > 10)
<generator object <genexpr> at 0x05570E10>
>>> [x for x in nums if x > 10]
[12, 15, 31]
```
(repetimos la list comprehension abajo para que se vea bien la comparación).

[Esta página](https://medium.freecodecamp.org/python-list-comprehensions-vs-generator-expressions-cef70ccb49db) incluye más info sobre la comparación entre list comprehensions y generator expressions.

<br/>

## Strings
Python incluye varias herramientas para trabajar con Strings. Muchos son métodos, pues los Strings son objetos, existe una clase String.

Un catálogo completo de las operaciones que soportan los Strings puede encontrarse en [la documentación de Python 3](https://docs.python.org/3/library/stdtypes.html#string-methods).

**Importante**  
Los Strings son *inmutables*, o sea, una vez construidos no se pueden modificar. Por lo tanto, *ninguna* operación sobre Strings es 'in-place'.

<br/>

### Caracteres especiales, *raw strings*
Los strings pueden incluir caracteres especiales, p.ej. `\n` que representa un salto de línea. Por eso, p.ej. `len('ho\nla')` es 5 (no 6), `'ho\nla'[2]` es `\n` y `'ho\nla'[3]` es `l`.

Para poner una barra invertida, se pone `\\`. P.ej. `'ho\\la'[2]` es la barra invertida, que se muestra como `\\`.

Otra opción es usar un *raw string*. Si adelante de las comillas se pone una `r`, entonces el string se toma literal. P.ej. `len(r'ho\nla')` es `6`, `r'ho\nla'[2]` es la barra invertida, y `r'ho\nla'[3]` es `n`.

<br/>

### Operaciones básicas
Las notaciones `[n]`, `[n:m]`, `+`, `*` funcionan para String con el mismo sentido que para listas.  
La notación `in` también, pero con una diferencia: detecta subsecuencias, no solamente elementos. Va con ejemplos:
```
>>> [8,3] in [2,8,3,5,1]
False
>>> "ep" in "pepita"
True
```

La función `len` y los métodos `count`, `index` también funcionan con String en forma análoga a con listas. Otra vez, `count` e `index` detectan también subsecuencias.

</br>

### Variantes de un String
La clase String incluye muchos métodos que devuelven variantes del String original.  
* Manejo de minúsculas y mayúsculas: `lower`, `upper`, `title`.
* Sacar espacios, rellenar con ceros o con un caracter a elección: `strip`, `lstrip`, `rstrip`, `zfill`, `center`, `ljust`, `rjust`.
* Reemplazar tabs por espacio: `expandtabs`.

</br>



