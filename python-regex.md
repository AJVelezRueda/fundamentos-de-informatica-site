<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Expresiones regulares
Son una herramienta que permite hacer búsquedas sofisticadas en Strings sin necesidad de escribir código. 
Python incluye un módulo de búsqueda mediante expresiones regulares en su biblioteca standard.  
En esta página vamos a describir algunas de sus características y potencialidad, a modo de introducción. Hay muchísima información disponible sobre el tema, en particular se puede consultar [la página sobre este tema en la documentación de Python 3](https://docs.python.org/3/library/re.html?highlight=regular%20expressions).

## Qué es una expresión regular.
Es un criterio de búsqueda sobre Strings, que se especifica mediante otro String.
Si un String se corresponde con el criterio que define una expresión regular, se dice que el String *hace match* con (o *matchea*) la expresión. Equivalentemente, se dice que la expresión *acepta* al String.

Un ejemplo sencillo de expresión regular es `"X(.*)Y"`. Esta expresión acepta cualquier String que empiece con X y termine con Y. 
P.ej., los strings `"XabkeY"` y `"XXXYYY"` matchean la expresión, lo que no sucede con ninguno de estos: `"alfonsina"`, `"atgX49"`, `"YalfaX"`, `"aaXbbbYj"`. 

Notar en particular el último ejemplo: `"aaXbbbYj"` incluye una subsecuencia que matchea la expresión regular. En este caso, el String no matchea la expresión regular, pero tiene un substring (una subsecuencia) que sí lo hace. 
Un String podría incluir varios matcheos de una expresión regular, en este caso un ejemplo sería `"aaXbbffYcccXdefYqqqq"`.

Intuitivamente, la expresión `"X(.*)Y"` se puede leer así: "una X, después una cantidad indeterminada de caracteres cualesquiera, y finalmente una Y". El punto indica "cualquier caracter" y el asterisco "una cantidad indeterminada". 
Volveremos sobre esto más adelante.

<br/>

## Usos de una expresión regular en Python
La forma más sencilla para usar expresiones regulares en Python es mediante el módulo `re` incluido en la biblioteca standard. Ergo, debemos incorporar este módulo:
```
import re
```

Este módulo incluye varias funciones para hacer consultas de matcheo. Veamos algunas.

**fullmatch**  
recibe una expresión regular (llamada "pattern" en la página de documentación referida arriba) y un String. Si el String, completo, hace match, entonces devuelve un objeto *match*, del que hablaremos un poco más tarde. Caso contrario, devuelve `None`, que es el *valor nulo* en Python. 

Por lo tanto, para preguntar si hay match, lo que consultamos es si el resultado de `fullmatch` es algo distinto de `None`.
Van algunos ejemplos:
```
>>> re.fullmatch("X(.*)Y", "XabkeY") is not None
True
>>> re.fullmatch("X(.*)Y", "atgX49") is not None
False
>>> re.fullmatch("X(.*)Y", "aaXbbbYj") is not None
False
>>> re.fullmatch("X(.*)Y", "XabkeYhola") is not None
False
```

<br/>

**match**  
parecido a `fullmatch`. La diferencia es que acepta que el match se haga sobre una subsecuencia *inicial* del String. Veamos cómo se porta con los mismos casos evaluados arriba.
```
>>> re.match("X(.*)Y", "XabkeY") is not None
True
>>> re.match("X(.*)Y", "atgX49") is not None
False
>>> re.match("X(.*)Y", "aaXbbbYj") is not None
False
>>> re.match("X(.*)Y", "XabkeYhola") is not None
True
```

La diferencia está en el último caso: el String `XabkeYhola` tiene una subsecuencia inicial, `XabkeY`, que hace match con la expresión `X(.*)Y`.

<br/>

**search**  
otra variante, ahora se acepta un match en cualquier subsecuencia del String, no se pide que esté al principio. Veamos:
```
>>> re.search("X(.*)Y", "XabkeY") is not None
True
>>> re.search("X(.*)Y", "atgX49") is not None
False
>>> re.search("X(.*)Y", "aaXbbbYj") is not None
True
>>> re.search("X(.*)Y", "XabkeYhola") is not None
True
```

<br/>

## Más información acerca de los matches
Usando las operaciones que detectan matches sobre una parte del String, podemos obtener cuál es la subsecuencia aceptada por la expresión regular. Para eso usamos el *match object* que devuelven estas operaciones. 

A este objeto le podemos pedir el `group`, con dos variantes que ... creemos que se ve más fácil con un ejemplo.
```
>>> re.search("X(.*)Y", "aaXbbbYj").group(0)
'XbbbY'
>>> re.search("X(.*)Y", "aaXbbbYj").group(1)
'bbb'
```

O sea, con `group(0)` obtenemos la subsecuencia entera, incluyendo los delimitadores izquierdo y derecho (respectivamente, la `X` y la `Y`); mientras que `group(1)` nos da la subsecuencia sin incluir los delimitadores.

Un comentario sintáctico: en la expresión `re.search("X(.*)Y", "aaXbbbYj").group(1)`, el `group` se lo estamos pidiendo *al resultado* que entrega `search`. Esto es importante entenderlo, ampliaremos al hablar de programación orientada a objetos.

<br/>

## Un detalle: matches exteriores o interiores
Evaluemos este caso:
```
>>> re.search("X(.*)Y", "aaXbbbYjjXtaggaYpp").group(1)
'bbbYjjXtag'
```
Cabe la pregunta de por qué el resultado no es `bbb`, que también es una subsecuencia encerrada entre una `X` y una `Y`.

Para responder, notemos que el String incluye *tres* matches de la expresión regular, a saber: `XbbbY`, `XtaggaY` y `XbbbYjjXtaggaY`. El último incluye propiamente a los otros dos, llamémoslo *externo*.

Ahora podemos dar una respuesta: la expresión regular `X(.*)Y` prioriza los matches externos. Si queremos obtener, en este caso, el primer match interno, debemos usar la variante `X(.*?)Y`. El signo de interrogación siguiendo a un asterisco especifica la preferencia por matches internos.

Veamos:
```
>>> re.search("X(.*?)Y", "aaXbbbYjjXtaggaYpp").group(1)
'bbb'
```
Efectivamente, obtuvimos el primer match interno.

En la documentación de Python, y probablemente en otras fuentes, la preferencia por los matches externos se conoce como "greedy matching", y aquella por los matches internos como "non-greedy matching" o "minimal matching".

<br/>

## Obtener todos los matches
Si un String incluye varios matches de una misma expresión regular, las funciones `findall` y `finditer` permiten obtener todos los substrings correspondientes.

La función `findall` es la más fácil de usar, devuelve una lista de los substrings:
```
>>> re.findall("X(.*?)Y", "aaXbbbYjjXtaggaYpp")
['bbb', 'tagga']
```
Como se ve en el ejemplo, obtenemos las subsecuencias sin los delimitadores, análogo a la variante `group(1)` que usamos con `search`.

Por su parte, la función `finditer` devuelve un iterador de *match objects*, a cada uno de ellos le podemos pedir `group(0)` o `group(1)`. Para obtener la misma lista que devuelve `findall`, podemos hacer
```
>>> [x.group(1) for x in re.finditer("X(.*?)Y", "aaXbbbYjjXtaggaYpp")]
['bbb', 'tagga']
```

<br/>

## Variantes en expresiones regulares
Hasta ahora trabajamos con solamente dos expresiones regulares, que aceptan strings que empiecen y terminen con delimitadores determinados.

Podemos estar interesados solamente en las subsecuencias con delimitadores que tengan una determinada *longitud*, o un rango de longitudes. P.ej. 

```
>>> re.findall("X(.*?)Y","aaXbbbYjjXtaggaYppXtctcYagagact")
['bbb', 'tagga', 'tctc']
>>> re.findall("X(.{4})Y","aaXbbbYjjXtaggaYppXtctcYagagact")
['tctc']
>>> re.findall("X(.{1,4})Y","aaXbbbYjjXtaggaYppXtctcYagagact")
['bbb', 'tctc']
```
El String `"aaXbbbYjjXtaggaYppXtctcYagagact"` incluye tres subsecuencias internas delimitadas por `X` e `Y`, de 3, 5 y 4 caracteres. En el segundo `findall` se piden las subsecuencias de exactamente 4 caracteres, en el tercero las que tienen entre 1 y 4.

Otra opción es buscar solamente ciertos caracteres, en lugar de cualquier caracter entre los delimitadores. P.ej. 
```
>>> re.findall("X((a|c|t|g)*)Y","aaXbbbYjjXtaggaYppXtctcYagagact")
[('tagga', 'a'), ('tctc', 'c')]
```
aquí se buscan solamente las cadenas delimitadas por X e Y que incluyan solamente las letras `a`, `c`, `g` o `t`. 
En este punto debo hacer una confesión: no termino de entender por qué evalúa a una lista de pares, y definitivamente no sé cómo arreglarlo. Para obtener el resultado análogo a las otras expresiones, pues deberé trabajar con lo que `findall` decide darme:
```
>>> [x[0] for x in re.findall("X((a|c|t|g)*)Y","aaXbbbYjjXtaggaYppXtctcYagagact")]
['tagga', 'tctc']
```

Finalmente mencionamos que los delimitadores pueden tener más de un caracter, p.ej.
```
>>> re.findall("ag(.*?)ct","aaXbbbYjjXtaggaYppXtctcYagagact")
['gaYppXt', 'aga']
```

Hay una multitud de otras variantes, que se pueden consultar en la documentación y en otros tutoriales.

<br/>

# Construcción dinámica de expresiones regulares
Imaginemos que queremos armar una función que devuelva las subsecuencias de un String que hacen match con una expresión regular delimitada, pero donde los delimitadores sean variables.
Digamos una función `delimitedParts` que recibe el String a analizar y los delimitadores, p.ej. 
```
>>> delimitedParts('aaaFbbbGrefHadxFacacgGxxxFsHwGu', 'F', 'G')
['bbb', 'acacg', 'sHw']
>>> delimitedParts('aaaFbbbGrefHadxFacacgGxxxFsHwGu', 'G', 'H')
['ref', 'xxxFs']
```

La función `delimitedParts` se puede resolver usando una expresión regular ... que debe formarse a partir de los valores de los parámetros segundo y tercero. En los ejemplos, las expresiones deben ser `F(.*?)G` y `G(.*?)H` respectivamente.

Afortunadamente, las expresiones regulares se manejan como Strings, que se pueden ensamblar dentro de la función:
```
def delimitedParts(theString,start,end):
    return re.findall(start + '(.*?)' + end, theString)
```

o lo que es equivalente
```
def delimitedParts(theString,start,end):
    regex = start + '(.*?)' + end
    return re.findall(regex, theString)
```

<br/>

## Reemplazos masivos usando expresiones regulares
La función `sub` permite reemplazar todos los matchs de una expresión regular en un String por otro String, que puede hacer incluso referencia al match.
Me limito a dejar un ejemplo, consultar los detalles en la documentación.
```
>>> re.sub('X(.*?)Y', r'Y\1X', 'alfaXeeejYlaXlaYjj')
'alfaYeeejXlaYlaXjj'
```
... o sea, se invirtieron los delimitadores en las secciones delimitadas por X e Y.







