<style>
.page-header {
	padding-bottom: 50px;
	padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  


# Ejercicio a entregar - modelo de compuestos y medios químicos
Se trata de desarrollar un modelo de compuestos y medios químicos, con características muy limitadas, y seguramente con errores, debidos a la ignorancia del redactor.

Este modelo se debe construir siguiendo las ideas básicas de la programación orientada a objetos, según se describieron en el curso. 

<br/> 

## Condiciones de entrega
1. Deben incluirse tests de cada objetivo parcial, al menos los correspondientes a los ejemplos que se describen para cada uno.
1. La entrega se debe realizar mediante un repositorio git que incluya el código a entregar, y la documentación que se estime conveniente. Por lo tanto, el mail de entrega debería limitarse a consignar la URL del repositorio. Obviamente, el docente debe tener acceso a dicho repositorio, al menos de lectura.  
Se pide usar uno entre github, bitbucket o gitlab, que son los repositorios en los que este docente tiene cuenta.
1. Para considerarse aprobada, una entrega debe incluir, al menos, todas las etapas salvo la última, que se refiere a las reacciones químicas. Lo indicado como *opcionales* en cada etapa no se incluye dentro de este alcance mínimo.

Se recomienda fuertemente realizar el desarrollo etapa por etapa. De hecho, la clase definida en cada etapa se utiliza en las siguientes.

<br/> 

## Elemento
Desarrollar la clase `Elemento`, que describe un elemento químico; en rigor, su isótopo más usual.
Deben contemplarse las siguientes consultas: `cantProtones()`, `cantNeutrones()`, `cantElectrones()`, `numeroAtomico()`, `pesoAtomico()`, `valencia()`, `simbolo()`.  
Considerar como peso atómico simplemente la suma de cantidades de protones y de neutrones.

Así, un objeto que represente al elemento oxígeno deberá exhibir este comportamiento:

| Expresión | Resultado |
| --- | --- |
| `oxigeno.cantProtones()` | 8 |
| `oxigeno.cantNeutrones()` | 8 |
| `oxigeno.cantElectrones()` | 8 |
| `oxigeno.numeroAtomico()` | 8 |
| `oxigeno.pesoAtomico()` | 16 |
| `oxigeno.valencia()` | 4 |
| `oxigeno.simbolo()` | "O" |

Los tests deben incluir al oxígeno y al hidrógeno, teniendo en cuenta que el isótopo más usual del hidrógeno no tiene ningún neutrón, siendo 1 su peso atómico. Tener en cuenta también que p.ej. para el flúor, el isótopo más usual tiene 10 neutrones y sólo 9 protones. Ergo, la cantidad de neutrones no puede deducirse de la de protones.

**Atención**  
No incluir, en la definición de la clase `Elemento`, más atributos de los necesarios, ni tampoco menos.

<br/>

## Tabla periódica
Desarrollar la clase `TablaPeriodica`, que debe responder a las siguientes operaciones: 
* `agregarElemento(elemento)`: agrega un elemento a la tabla.
* `elementos()`: devuelve la lista con los elementos agregados.
* `elementoS(simbolo)`: devuelve el elemento de la tabla que tenga el símbolo indicado, o `None` si no hay ningún elemento con tal símbolo.
* `elementoN(numero)`: análogo a `elementoS`, buscando por número atómico en lugar de por símbolo.

Así, una tabla periódica a la que se hubieran agregado hidrógeno, oxígeno, carbono y nitrógeno, debe exhibir este comportamiento:

| Expresión | Resultado |
| --- | --- |
| `len(tabla.elementos())` | 4 |
| `tabla.elementoS('C').numeroAtomico()` | 6 |
| `tabla.elementoN(7).pesoAtomico()` | 14 |

dado que `tabla.elementoS('C')` es el carbono, y `tabla.elementoN(7)` es el nitrógeno.

**Sugerencia para lo que sigue**  
Definir una variable `tabla`, que referencie a una instancia de `TablaPeriodica` que tenga los elementos más comunes ya agregados, para poder importarla en los tests de las etapas siguientes.
También se pueden definir variables correspondientes a los elementos más usuales, p.ej. `oxigeno`, `hidrogeno`, etc..

### Opcionales
Que sólo agregue un elemento si no está ya en la lista, de acuerdo a su símbolo.

<br/>

## Compuesto
Desarrollar una clase `Compuesto`. Un compuesto se construye en dos fases: primero se agregan los átomos, y luego los enlaces.
Para cada átomo se indican: el elemento, y el nombre del átomo dentro de la molécula. Estos nombres se usan para definir los enlaces.  
De cada compuesto nos va a interesar, también, la fórmula.

En este ejemplo se define al compuesto amoníaco (se supone que la variable `tabla` hace referencia a una tabla periódica)
```
	nh3 = Compuesto('NH3')
	nh3.agregarAtomo(tabla.elementoS("N"), "N1")
	nh3.agregarAtomo(tabla.elementoS("H"), "H2")
	nh3.agregarAtomo(tabla.elementoS("H"), "H3")
	nh3.agregarAtomo(tabla.elementoS("H"), "H4")
	nh3.enlazar("N1", "H2")
	nh3.enlazar("N1", "H3")
	nh3.enlazar("N1", "H4")
```

**Atención**  
Se contemplan solamente enlaces covalentes.

El  modelo debe soportar estas operaciones: 
* sobre átomos y sus elementos: `cantAtomos()`, `atomosDe(elemento)`, `incluyeAtomo(nombre)`, `incluyeElemento(elemento)`, `elementosPresentes()`.  
¡OJO! lo que devuelva `elementosPresentes()` (lista, set o iterador) no puede tener repetidos.
* sobre enlaces: `cantEnlaces()`, `cantEnlacesAtomo(nombre)`.
* sobre masa: `masaMolar()`, `proporcionSobreMasa(elemento)`. 

Así, el compuesto `nh3` definido más arriba debería exhibir el siguiente comportamiento:

| Expresión | Resultado |
| --- | --- |
| `nh3.cantAtomos()` | 4 |
| `nh3.atomosDe(tabla.elementoS('H'))` | `["H1", "H2", "H3"]` |
| `nh3.incluyeAtomo("N1")` | True |
| `nh3.incluyeAtomo("N4")` | False |
| `nh3.incluyeElemento(tabla.elementoS('N'))` | True |
| `nh3.incluyeElemento(tabla.elementoS('O'))` | False |
| `[elem.simbolo() for elem in nh3.elementosPresentes()]` | `["N","H"]` |
| `nh3.cantEnlaces()]` | 3 |
| `nh3.cantEnlacesAtomo("H2")]` | 1 |
| `nh3.masaMolar()]` | 17 |
| `nh3.proporcionSobreMasa(tabla.elementoS('N'))` | 0.8235 |

**Nota**  
Los enlaces dobles se pueden registar, sencillamente, como dos enlaces. P.ej., el dióxido de carbono puede crearse así:
```
	co2 = Compuesto('CO2')
	co2.agregarAtomoDe(tabla.elementoS('O'), "O1")
	co2.agregarAtomoDe(tabla.elementoS('O'), "O2")
	co2.agregarAtomoDe(tabla.elementoS('C'), "C3")
	co2.enlazar("C3", "O1")
	co2.enlazar("C3", "O1")
	co2.enlazar("C3", "O2")
	co2.enlazar("C3", "O2")
```

**Sugerencia para lo que sigue**  
Definir variables correspondientes a compuestos comunes que puedan utilizarse en test de esta etapa y de las siguientes. P.ej. `agua`, `metano`, `nh3`, `co2`.  
Como ejemplo con más átomos, enlaces y elementos intervinientes, se puede usar p.ej. la cisteina.


### Opcionales
**Formas compactas para crear compuestos**  
Agregar los métodos `agregarAtomos` y `enlazarConVarios`, de forma tal que la creación de una molécula de amoníaco pueda reducirse a lo siguiente:
```
	nh3 = Compuesto('NH3')
	nh3.agregarAtomo(tabla.elementoS("N"), "N1")
	nh3.agregarAtomos(tabla.elementoS("H"), ["H2", "H3", "H4"])
	nh3.enlazarConVarios("N1", ["H2", "H3", "H4"])
```

Adicionalmente, se puede lograr que los nombres de átomo en una molécula se generen automáticamente. Esto nos permitiría llegar a una creación aún más compacta:
```
	nh3 = Compuesto('NH3')
	nh3.agregarAtomo(tabla.elementoS("N"))
	nh3.agregarAtomos(tabla.elementoS("H"), 3)
	nh3.enlazarConVarios("N1", ["H2", "H3", "H4"])
```

<br/>

**Validación de enlaces**  
Lograr que los compuestos soporten las siguientes operaciones: 
* `enlacesOK()`: indica si la definición de enlaces es correcta. Posibles causas para que no sea así: incluir, en un enlace, un nombre de átomo que no pertenece al compuesto (p.ej. en el amoníaco si hiciéramos `nh3.enlazar("N1", "C5")`); o que un átomo tenga más enlaces que su valencia (p.ej. si en lugar de enlazar N1 con H3, enlazáramos por error H2 con H3, entonces H2 tendría más enlaces que su valencia).
* `atomosConEnlacesSobrantes()`: devuelve la lista de átomos que tienen más enlaces que su valencia.
* `atomosConEnlacesDisponibles()`: devuelve la lista de átomos que tienen menos enlaces que su valencia, por lo que se pueden agregar enlaces en los que intervenga el átomo. P.ej. en el caso erróneo mencionado más arriba tendríamos `nh3.atomosConEnlacesDisponibles() = ['N1']`.

<br/>

**Más información sobre enlaces**  
Lograr que los compuestos soporten las siguientes operaciones: 
* `conQuienesEstaEnlazado(nombre)`: devuelve una lista con los nombres de los átomos con los que está enlazado el átomo indicado. P.ej. para el amoníaco tenemos `nh3.conQuienesEstaEnlazado("H2")] = ["N1"]` y`nh3.conQuienesEstaEnlazado("N1")] = ["H1", "H2", "H3"]`.
* `estanEnlazados(elem1, elem2)`: indica si el compuesto incluye al menos un enlace entre átomos de los elementos indicados.

<br/>

## Medio
Un *medio* incluye varios compuestos, para cada uno se especifica cuántos moles hay.

P.ej. un medio que incluye agua, amoníaco, metano y dióxido de carbono se define así:
```
medioRaro = Medio()
medioRaro.agregarComponente(agua, 100)
medioRaro.agregarComponente(nh3, 6)
medioRaro.agregarComponente(metano, 20)
medioRaro.agregarComponente(co2, 14)
```

Si se agrega a posteriori una cantidad de moles de un compuesto que ya está presente, entonces esta cantidad *se suma* a la que ya contiene. P.ej. agregando lo siguiente a la definición anterior:
```
medioRaro.agregarComponente(nh3, 15)
```
se *aumenta* la cantidad de amoníaco, de 6 a 21 moles.

El modelo de un medio debe soportar las siguientes operaciones:
* `masaTotal()`, considerando la cantidad de moles de cada elemento.
* `elementosPresentes()`, considerando todos los compuestos involucrados.  
¡OJO! lo que devuelva (lista, set o iterador) no puede tener repetidos.
* `compuestosPresentes()`, también sin repetidos.
* `cantMolesElemento(elem)`, la cantidad total de moles del elemento indicado en el medio, considerando todos los compuestos incluidos y sus cantidades.
* `masaDeCompuesto(comp)` y `masaDeElemento(elem)`, los totales para el medio.
* `proporcionElementoSobreMasa(elem)` y `proporcionCompuestoSobreMasa(comp)`.

P.ej. en el medio definido tenemos:

| Propiedad | Valor | 
| --- | --- |
| masa total | 3093 gramos |
| elementos presentes | hidrógeno, oxígeno, nitrógeno y carbono |
| compuestos presentes | agua, amoníaco, metano y dióxido de carbono | 
| cantidad de moles por elemento | oxígeno: 128; hidrógeno: 343 |
| masa por compuesto | agua: 1800 gramos; amoníaco: 357 gramos |
| masa por elemento | oxígeno: 2048 gramos; carbono: 408 gramos |
| proporción de un compuesto sobre masa | agua: 0.5819 |
| proprción de un elemento sobre masa | oxígeno: 0.6621; hidrógeno: 0.1108 |

<br/>

### Opcionales
Lograr que los medios soporten estas operaciones:
* `escalar(numero)`: multiplica las cantidades de cada componente por el número indicado. P.ej. `medioRaro.escalar(3)` pasa la cantidad de agua de 100 moles a 300, la de amoníaco de 21 moles a 63, etc.; mientras que `medioRaro.escalar(0.5)` deja al medio con 50 moles de agua, 10.5 de amoníaco, etc..
* `incorporarMedio(otroMedio)`: suma a las cantidades del medio que recibe la operación, las incluidas en `otroMedio`.
* `masMedio(otroMedio)`: devuelve **un nuevo** medio, que es la suma entre el medio que recibe la operación y `otroMedio`. Ni el medio que recibe la operación no debe modificarse ni `otroMedio` deben modificarse.

<br/>

## Descripción textual de medio
Se define el siguiente formato para describir textualmente un medio: 
```
[form1][form2]...[formn]
```
donde `form1`, ..., `formn` son las fórmulas de los compuestos que conforman el medio. Una fórmula indica la presencia de *un mol* del compuesto: para indicar más de un mol, se repite la fórmula tantas veces como sea necesario.  
Los corchetes se incluyen en la descripción.

P.ej. este String 
```
[H2O][CO2][H2O][CH4]
```
describe un medio que incluye dos moles de agua, una de dióxido de carbono y una de metano.

<br/>

Definir una clase `DescripcionMedio` que maneje descripciones definidas de esta forma. El String se puede pasar como parámetro cuando se crea una instancia, p.ej. 
```
miDescripcion = DescripcionMedio("[H2O][CO2][H2O][CH4]")
```

Las descripciones deben soportar las siguientes operaciones:
* `apareceCompuesto(comp)`: indica si un compuesto está presente en la descripción.
* `molesCompuesto(comp)`: indica cuántos moles de un compuesto incluye la descripción.
* `quienesAparecen(listaDeCompuestos)`: indica cuáles de los compuestos incluidos en la lista, aparecen en la descripción.
* `agregarAMedio(medio, compuesto)`: agrega al `medio`, la cantidad de moles del `compuesto` que están incluidas en la descripción.

P.ej. para la descripción definida recién, tenemos

| Propiedad | Valor | 
| --- | --- |
| `miDescripcion.apareceCompuesto(agua)` | True |
| `miDescripcion.apareceCompuesto(co2)` | True |
| `miDescripcion.apareceCompuesto(nh3)` | False |
| `miDescripcion.molesCompuesto(agua)` | 2 |
| `miDescripcion.molesCompuesto(co2)` | 1 |
| `miDescripcion.molesCompuesto(nh3)` | 0 |
| `miDescripcion.quienesAparecen([agua, nh3, metano])` | una lista o iterador que incluye `agua` y `metano` |

donde `agua`, `metano`, `co2` y `nh3` son variables que referencian a los compuestos correspondientes.

Finalmente, describimos el efecto de la operación `agregarAMedio`, aplicada sobre el `medioRaro` definido en la etapa previa.

| Operación | Efecto | 
| --- | --- |
| `miDescripcion.agregarAMedio(medioRaro,agua)` | El agua en `medioRaro` aumenta en dos moles, pasando de 100 a 102 |
| `miDescripcion.agregarAMedio(medioRaro,metano)` | El metano en `medioRaro` aumenta en un mol, pasando de 20 a 21 |
| `miDescripcion.agregarAMedio(medioRaro,nh3)` | No se produce ningún efecto, porque `miDescripcion` no incluye ningún mol de amoníaco |

<br/>

### Agregados
**Más operaciones**  
Lograr que las instancias de `DescripcionMedio` soporten estas operaciones:
* `compuestosDesconocidos(listaCompuestos)`: devuelve la lista de las fórmulas presentes en la descripción, que no coinciden con ninguno de los compuestos en `listaCompuestos`.  
P.ej. `miDescripcion.compuestosDesconocidos([agua,nh3,metano])` devuelve `["CO2"]`, porque la lista suministrada no incluye al dióxido de carbono, que sí está presente en la descripción.
* `agregarTodosAMedio(medio, listaCompuestos)`, que agrega al medio todos los compuestos presentes en la descripción que estén en `listaCompuestos`. 
* `agregarTodosAMedioConEscala(medio, listaCompuestos, escala)`, idem anterior, multiplicando las cantidades a agregar según la `escala`.  
P.ej. `miDescripcion.agregarTodosAMedioConEscala([agua,nh3,metano], 100)` agrega 200 moles de agua y 100 de metano.

**Descripciones con cantidades**  
Ajustar el modelo para que soporte descripciones donde luego de cada fórmula se indique la cantidad de moles, como un número entre paréntesis. P.ej. 
```
[H2O](1000)[CO2](50)[CH4](25)
```
describe un medio con 1000 moles de agua, 50 de dióxido de carbono y 25 de metano.  
Deben soportarse todas las operaciones descriptas en esta etapa.

Queda a criterio del desarrollador si modificar la clase `DescripcionMedio` para que soporte descripciones con o sin cantidades, o definir una nueva clase para las descripciones con cantidades.

<br/>

## Reacciones químicas
Agregar al modelo las *reacciones químicas*. Una reacción química se define a partir de sus conjuntos de reactivos y de productos.  
Se recomienda crear una nueva clase `ReaccionQuimica`.

Se puede asumir que en la reacción intervienen cantidades iguales de todos los reactivos, generándose las mismas cantidades de cada producto.

Se deben soportar las siguientes operaciones:
* `sePuedeAplicar(medio)`: indica si el medio incluye todos los reactivos de la reacción, de forma tal que la reacción se pueda llevar a cabo.
* `maximoMoles(medio)`: indica cuántos moles de cada reactivo pueden participar, como máximo, de aplicarse la reacción en el medio indicado.  
P.ej. si los insumos de una reacción son agua y metano, en un medio que incluya 1000 moles de agua y 40 de metano, `maximoMoles` debe devolver 40, que es la cantidad máxima de moles de cada insumo que pueden intervenir en la reacción.
* `aplicar(medio,proporcion)`: aplica la reacción al medio indicado, modificando su composición: se consumen los reactivos y se generan los productos. La `proporcion` es respecto de la cantidad máxima de moles que podría participar.  
En el ejemplo anterior, `aplicar(medio,0.5)` haría reaccionar (y por lo tanto consumir) 20 moles de agua y 20 de metano, generando 20 moles de cada producto.



















