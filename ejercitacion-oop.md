<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Ejercitación - programación con objetos

## Aves y ornitólogos
Definir un modelo de gorriones, de los cuales nos interesa conocer dos medidas conocidas como CSS (coeficiente de serenidad silenciosa, que algunas mentes malignas han bautizado como "coeficiente sin sentido"), CSSP y CSSV (como el CSS pero "pico" y "veces"). 
El CSS resulta de dividir la cantidad total de kilómetros que vuela desde que se lo comienza a estudiar, por la cantidad total de gramos de comida que ingiere. El CSSP es la misma división pero considerando solamente lo que voló la vez que más voló y lo que comió la vez que más comió. El CSSV es otra vez la misma idea, respecto de la *cantidad* de veces que voló y comió.
Si un gorrión nunca comió, los coeficientes deben ser `None`.

Un gorrión se considera en equilibrio si su CSS está entre 0.5 y 2.

Cada *ornitólogo* tiene un conjunto de aves bajo estudio. Cada una de estas aves puede ser un gorrión, o una golondrina de acuerdo a lo descripto en [la página inicial sobre programación con objetos](./oop-intro.md).
Un ornitólogo somete, cada vez que lo decide, a cada una de las aves que tiene en estudio a una rutina que consiste en: hacerla comer 80 gramos, hacerla volar 70 kms, y finalmente hacerla comer otros 10 gramos.

Se propone:
* implementar la clase `Gorrion`, de forma tal que acepte las operaciones `comer(gramos)`, `volar(kms)`, `css()`, `cssp()`, `cssv()`, y `estaEnEquilibrio()`. Comprobar que dichas operaciones tienen el comportamiento esperado.
* implementar la clase `Ornitologo`, de forma tal que acepte las operaciones `estudiarAve(ave)`, `avesEnEstudio()`, `realizarRutinaSobreAves()`, `avesEnEquilibrio()`. Realizar rutina es ejecutar la rutina descripta más arriba sobre cada ave que tiene en estudio. Las aves en equilibrio son aquellas aves, entre las que el ornitólogo tiene en estudio, que responden `True` cuando se les consulta `estaEnEquilibrio()`.
* comprobar el código que se escribió con esta secuencia:
    - definir un ornitólogo, dos golondrinas y dos gorriones, 
    - inicializar las aves con valores conocidos,
    - decirle al ornitólogo que estudie una de las golondrinas y los dos gorriones,
    - decirle al ornitólogo que realice su rutina sobre aves,
    - verificar los valores de las cuatro aves definidas, para las tres que tiene en estudio el ornitólogo estos valores deberían haber cambiado, para la otra ave no.

<br/>

**Desafío especial**  
Lograr que la rutina que un ornitólogo impone a las aves que estudia sea configurable, y modificable sobre un ornitólogo ya existente.  
Pensar cómo se puede indicar esta configuración, qué elemento se le puede pasar a un ornitólogo que describa la rutina que hay que ejecutar.

<br/>


## Atención de animales
Realizar una implementación del ejercicio 4 de la guía 5 en [la página de programación con objetos 1 de la UNQ](https://objetos1wollokunq.gitlab.io/material/#guides), el de atención de animales.

Luego, implementar el ejercicio 1 de la guía 7 del mismo sitio, que plantea agregados al mismo dominio.


## Átomos, medios, reacciones

### Átomos y sus enlaces
Implementar un modelo de un átomo del que se pueda conocer: 
* cantidad de protones y de electrones.
* valencia (o sea, cantidad de electrones que pueden generar enlaces).
* peso atómico.

Incluir la posibilidad de *enlazar* dos átomos, utilizando un enlace de cada uno. Debe habilitarse la posibilidad de consultar, para un átomo, con qué otros átomos está enlazado directamente.
Notar que es importante conocer, para cada átomo, la cantidad de *electrones disponibles para enlace*. P.ej. si un átomo tiene valencia 3, y está enlazado con otros dos átomos, entonces le queda sólo un electrón disponible para enlace.

Si se estima conveniente, se puede pensar que los electrones que pueden enlazarse en un átomo llevan una numeración correlativa, para poder indicar con precisión cuáles de los electrones de cada átomo quedan enganchados en un enlace. P.ej. si un átomo A tiene valencia 2 y otro átomo B 4, poder indicar que se enlazan el electrón 1 del A con el 3 del B. 
De esta forma, se puede informar a posteriori que los electrones que quedan disponibles para enlace en el átomo B son [1,2,4].

<br/>

**Nota**  
Tal vez este modelo asume que todos los enlaces son covalentes. Sepan comprender, y eventualmente ayudar, a un ignorante en ciencias naturales.

<br/>

### Elementos e isótopos
Agregar al modelo los elementos químicos y sus isótopos. 
De cada elemento pueden interesar: el número atómico, el símbolo, el nombre, la valencia de sus átomos. 
De cada isótopo: el elemento (del cual a su vez se puede obtener la cantidad de protones), la cantidad de neutrones, la valencia de sus átomos, el peso atómico.

Modificar el modelo de átomos del punto anterior para que cada átomo mantenga una referencia a su isótopo (y este, a su vez, a su elemento). De esta forma, no es necesario que cada átomo recuerde p.ej. la cantidad de protones o de electrones; puede pedirle estos datos al isótopo.

Los átomos se pueden *crear* a partir de su isótopo. P.ej.:
```
# el carbono es el elemento 6, tetravalente
carbono = quim.Elemento(6, 'Carbono', 'C', 4)
# el carbono 14 es un isótopo del carbono, que tiene 8 neutrones
carbono14 = quim.Isotopo(carbono, 8)
# a partir del isótopo, creo un átomo de carbono 14
unAtomo = carbono14.crearAtomo()
```

<br/>

Para lo que sigue, es conveniente que también se pueda acceder a los isótopos de un elemento a partir del elemento. P.ej.
```
carbono = quim.Elemento(6, 'Carbono', 'C', 4)
# creo el isótopo carbono 14, en este acto se engancha el isótopo al elemento
quim.Isotopo(carbono, 8)
# despues puedo obtener el isótopo a partir del elemento
carbono14 = carbono.isotopo(14)
```

**Nota**  
Este modelo asume que la cantidad de protones y de electrones de un átomo coincide con el número atómico de su elemento. Espero haber entendido bien.

<br/>

### Tabla periódica 
Definir un diccionario global al que se pueda obtener un elemento a partir de su símbolo (o su número atómico, como se prefiera). P.ej.
```
# obtengo el carbono, y el carbono 14, a partir de la tabla periódica
carbono = tablaPer['C']
carbono14 = carbono.isotopo(14)
```


<br/>

### Moléculas y compuestos
Agregar al modelo las moléculas. Una molécula está compuesta por un conjunto de átomos, que pueden tener enlaces entre ellos. Notar que los enlaces son mantenidos por los átomos, el modelo de molécula puede limitarse a tener referencias a los átomos que la componen.

Lograr que al modelo de una molécula se pueda consultar: de qué elementos / isótopos se compone, cuántos átomos incluye de un elemento / átomo, el peso molar, los átomos que tienen al menos un enlace disponible.

<br/>
Agregar también los *compuestos*. La principal función de un compuesto es generar moléculas, que incluyen los átomos enlazados correctamente.
Generar una clase para cada compuesto, dado que el código para crear moléculas difiere de compuesto en compuesto. P.ej.
```
# tengo la clase Agua, creo una molécula
>>> moleculaDeAgua = quim.Agua().crearMolecula()
>>> moleculaDeAgua.cantidadAtomos()
3
```

Conviene que cada compuesto me sepa decir su nombre.
```
>>> quim.Agua().nombre()
"Agua"
```

<br/>

Una mejora sería que no fuera necesario crear una nueva instancia del compuesto:
```
moleculaDeAgua = quim.Agua.crearMolecula()
```


### Macromoléculas
Agregar al modelo las *macromoléculas*, o sea, estructuras que se componen de moléculas (y eventualmente también átomos) enlazadas entre ellas.

Las macromoléculas pueden dar la misma información que una molécula.

Pensar si es posible que una misma clase, llamémosla `Estructura`, pudiera servirnos para modelar tanto moléculas como macromoléculas. De esta forma, un `Compuesto` nos serviría para construir cualquier estructura.


<!--
    Reacción: insumos: [Compuesto / Elemento / Isótopo], productos: [Compuesto / Elemento / Isótopo], puedeAplicarseSobre([Molecula / Macro / Atomo]), aplicarSobre([Molecula / Macro]) / puedeOcurrirEnMedio(Medio).
    Medio: componentes y cantidad de cada uno.
-->

