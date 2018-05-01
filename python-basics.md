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

### Bloque for
```
for variable in iterable: 
    bloque
```
Hay muchas opciones para iterable, entre ellas: listas, arrays, diccionarios, sets, `range` entre otras. 


range(min,max) te da un lindo iterable
while cond: block 
