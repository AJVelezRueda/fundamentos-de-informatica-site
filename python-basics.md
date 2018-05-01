<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

# Python: un pantallazo para arrancar

## Elementos iniciales
Variables y funciones.

## Algunas particularidades
En algunos aspectos, el comportamiento de Python difiere del de la mayor parte de los lenguajes de programación populares. Va una lista.
* No hay una sintaxis para declarar variables, quedan declaradas con el primer uso.
* La estructura de una sección de código se da por la indentación y el uso del símbolo dos-puntos. En muchos lenguajes, la estructura se define encerrando los bloques entre llaves.

<br/>

## Condicional
```
if condicion-1: 
    bloque 
elif condicion-2: 
    bloque
# puede haber varios bloques "elif"
else: 
    bloque
```
Al contrario de la mayor parte de los lenguajes, en Python no es necesario encerrar las condiciones entre paréntesis.

<br/>

## Estructuras de repetición

### Bloque `for`, en general
```
for variable in iterable: 
    bloque
```
Hay muchas opciones para iterable, entre ellas: listas, arrays, diccionarios, sets, `range` entre otras. 

### Bloque `for` usando `range`
La construcción `range` permite armar bloques que se repiten una cantidad determinada de veces, indexados por un entero.  
En este ejemplo muy sencillo, se hace iteración de 5 veces indexadas por los números 0 a 4.
```
for variable in range(5): 
    bloque
```

Si reemplazamos `range(5)` por
* `range(2,12)`: obtenemos 10 iteraciones, indexadas por los números 2 a 11 respectivamente.
* `range(2,12,2)`: obtenemos 5 iteraciones, indexadas por 2, 4, 6, 8, 10.

Se puede jugar con números negativos.

### Bloque `while`
```
while condicion:
    bloque
```


<br/>

## Una curiosidad cómoda: el operador ternario
```
<valorTrue> if <condicion> else <valorFalse>
```

P.ej. el resultado de 
```
3 if 'a' < 'b' else 4
```
es `3`, mientras que el de
```
3 if 'c' < 'b' else 4
```
es `4`.

Sirve para evitar la definición de variables, puede ser muy práctico.