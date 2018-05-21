<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Ejercitación - expresiones regulares

## Iniciales
Escribir funciones que, dado un String, permitan obtener

1. cuántas veces aparece el string `abc`. 
P.ej. aparece 2 veces en `xcabcb3sabc9`, y ninguna en `hola amigos mios`.

1. si *empieza* con un substring delimitado entre '<' y '>'.
Es el caso de `<presidente>`, `<presidente>pepe<secretario>lucia` y de `<secretario>lucia<presidente>pepe`; no así para `pepe<presidente>lucia<secretario>` ni para `hola amigos mios`.

1. si *es* un string delimitado entre '<' y '>'.
De los ejemplos del item anterior, solamente `<presidente>` cumple esta condición.

1. la lista de los substrings delimitados entre '<' y '>'.
P.ej. para `<presidente>pepe<secretario>lucia<tesorero>juana<medico>ana<sanitarista>hector`, debe devolver `['presidente', 'secretario', 'tesorero', 'medico', 'sanitarista']`.

1. la lista de los substrings delimitados entre '<' y '>', que tengan menos de 10 caracteres. En el ejemplo anterior, `['tesorero', 'medico']`.

1. la lista de los substrings delimitados entre '<' y '>', de exactamente 10 caracteres. En el ejemplo anterior, `['presidente', 'secretario']`.

1. la lista de los substrings delimitados entre comillas simples o dobles, donde se admite que un substring empiece con una y termine con la otra, p.ej. 
`"Nepomuceno'`. P.ej. si el String es `"Creta' es una isla de 'Grecia', capital "Heraklion", población 600000`, entonces lo que se busca es `['Creta', 'Grecia', 'Heraklion']`.

1. la lista de los substrings delimitados entre 'aa' y 'gg', que *no* incluyan ninguna 'c'. P.ej. en 'ttaatatggttaacatgg', debe tomar solamente 'tat', rechazando 'cat'.


## Para bucear en la documentaciónn
Escribir funciones que, dado un String, permitan resolver cada ua de las consignas siguientes. En estos casos, se requiere mirar un poco la documentación sobre expresiones regulares referenciada desde [la página correspondiente en este sitio](./python-regex.md).

1. si *termina* con un substring delimitado entre '<' y '>'.

1. la lista de los substrings delimitados entre '<' y '>' que *no* incluyan ninguna 'o'.
P.ej. para `<presidente>pepe<secretario>lucia<tesorero>juana<medico>ana<sanitarista>hector`, debe devolver `['presidente', 'sanitarista']`.

1. los pares de subsecciones delimitadas por, sucesivamente, una 'A', una 'B' y una 'C'. P.ej. `abxdAxxxByyyyzCtttAtBmC` tiene dos de estas subsecciones, con lo que el resultado esperado es `[('xxx', 'yyyyz'), ('t', 'm')]`.

1. devolver el resultado de *reemplazar* todas los substrings `agt` por `tca`. El método `sub` puede servir para esto.

1. devolver el resultado de *invertir* los delimitadores '<' y '>', o sea transformar las subsecciones delimitadas por '<' y '>' reemplazando los delimitadores por '>' y '<' respectivamente.


## Para pensar un poco
Escribir funciones que, dado un String, permitan resolver cada ua de las consignas siguientes. 
En algunos casos las expresiones regulares nos permiten solamente un "preprocesamiento", obteniendo una lista preliminar de resultados que luego debe ser analizada con otras herramientas. Para este procesamiento posterior, podrían ser útiles las list comprehension.

1. si incluye un substring de 3 letras, cada una de las cuales debe ser a, b ó c. Esto es, alcanza con incluir, p.ej, 'abc', 'cbc', 'aac', 'ccc'.

1. la lista de los substrings delimitados entre comillas simples o dobles, donde cada substring debe empezar y terminar con la misma comilla. P.ej. si el String es `"Creta' es una isla de 'Grecia', capital "Heraklion", población 600000`, entonces lo que se busca es `['Grecia', 'Heraklion']`.

1. obtener la secuencia de pares de caracteres en un String, "cortados" de a dos. P.ej. para "12345678", se busca `["12", "34", "56", "78"]`. 
Sugerencia: la expresión regular `(.{2})` puede ser útil.

1. lo mismo considerando *todos* los pares de caracteres consecutivos, no necesariamente en orden. P.ej. para "12345678", podría ser `["12", "34", "56", "78", "23", "45", "67"]`.
Sugerencia: considerar el String recibido sin el primer caracter.

1. lo mismo considerando *todos* los pares de caracteres consecutivos, y en el orden en que están en el String original. P.ej. para "12345678" hay que armar `["12", "23", "34", "45", "56",  "67", "78"]`. 
Sugerencia: tal vez sirva `zip`.

1. la cantidad de veces que se encuenta el par 'ag' en un String.

1. la cantidad de veces que se encuentra el par 'aa' en un String. 
Sugerencia: usar alguno de los ejercicios anteriores.

1. la lista de subsecuencias delimitadas por 'X' e 'Y', que incluyan estrictamente más 'a' que 'b'. P.ej. en `XbaaaYjXababYqXbabbbbaaYqXffeeY`, sólo hay que considerar `baaa`.

1. la lista de subsecuencias delimitadas por 'X' e 'Y', que incluyan la subsecuencia 'ab'. P.ej. para `XbaaaYjXababYqXbabbbbaaYqXffeeY`, hay que devolver `['abab', 'babbbaa']`.


## Expresiones dinámicas
1. Escribir la función `seccionesDelimitadas`, que dados un String y delimitadores, devuelve las substrings que están delimitados como se indica. P.ej. `seccionesDelimitadas('aaXbbbYcccXdeYff', 'X', 'Y')` debe devolver `['bbb', 'de']`.

1. Escribir la función `seccionesDelimitadasDeTamanio`, similar a la anterior pero con un parámetro adicional, que es la longitud de las subseciones buscadas. P.ej. `seccionesDelimitadasDeTamanio('aaXbbbYcccXdeYff', 'X', 'Y', 3)` debe devolver `['bbb']`.


## Ejercicio integrador
Se trata de "recortar" las secciones del ADN de un organismo que codifican genes. Esta especie es muy sencilla: cada gen viene precedido por el promotor próximo 'aaaggg', luego 5 nucleótidos que pueden ser cualesquiera, y luego el promotor núcleo 'tttccc'. Después viene el gen, que termina con el terminador, 'tctctcat'. El desafío es:

1. Armar una función que dada la secuencia de ADN, devuelva la lista de subsecuencias que corresponden a los genes.

1. Armar una función que recibe secuencia de ADN, promotor próximo, distancia entre promotores, promotor núcleo y terminador, y devuelve la lista de subsecuencias que corresponden a los genes.
