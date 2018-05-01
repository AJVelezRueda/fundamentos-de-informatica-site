<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Editores que pueden usarse para código Python

## Editores clásicos
P.ej. `vi` o `vim`.

## Editores modernos
P.ej. **Sublime Text**, **Atom** o **Visual Studio Code**.
Estos editores incluyen, o puede agregarse, soporte para el lenguaje que incluye coloreo por sintaxis, opciones de autocompletado, y tal vez algunas otras funcionalidades.

## PyCharm
Es un *entorno integrado de desarrollo*, o *IDE* para Python.  
Incluye varias capacidades relacionadas con el lenguaje, como coloreo, navegación por las definiciones, opciones de autocompletado que funcionan bastante bien, facilitación de cambios de nombre, y otros.  
También se puede ejecutar código, y tests automáticos, dentro del mismo entorno.

<br/>

# Entornos para ejecutar código Python

## Intérprete interactivo
Se arranca poniendo simplemente
```
> python
```
en línea de comando.

De esta forma, funciona como intérprete interactivo, también conocido como **REPL** (por *read / eval / print loop*).

Es una forma muy ágil de probar características del lenguaje.

Soporta el uso de bibliotecas (= módulos) en (al menos) dos formas: 
* Seteando la variable de entorno `PYTHONPATH`
* haciendo `import` en el prompt del REPL.

**Atención**  
Si se está probando un módulo propio y se lo modifica, se lo puede recargar sin salir del intérprete interactivo.
Para eso se usa el módulo `importlib`, o sea que una vez hay que poner
```
>>> import importlib
```
Este módulo incluye una función `reload` que hace lo que queremos:
```
>>> importlib.reload(<nombre-del-modulo>)
```



## Ejecución de un archivo
Se guarda el código a ejecutar en un archivo con extensión `.py`, y se arranca la ejecución poniendo
```
> python <nombre-de-archivo.py>
```
en línea de comando.

Se puede usar `PYTHONPATH` para incorporar bibliotecas.


## PyCharm
Como ya dijimos, se pueden ejecutar archivos Python desde PyCharm. Este IDE incluye un manejo de bibliotecas.
