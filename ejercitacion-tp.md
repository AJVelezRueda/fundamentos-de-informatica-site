<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  


# Ejercicio a entregar - modelo de compuestos y medios químicos
Se trata de desarrollar un modelo de compuestos y medios químicos, con características muy limitadas, y seguramente con errores, debidos a la ignorancia del redactor.

La consigna se describe mediante una secuencia de objetivos parciales. Se recomienda fuertemente tener en cuenta esta secuencia para desarollar el modelo.

Este modelo se debe construir siguiendo las ideas básicas de la programación orientada a objetos, según se describieron en el curso. 

<br/> 

## Condiciones de entrega
1. Deben incluirse tests de cada objetivo parcial, al menos los correspondientes a los ejemplos que se describen para cada uno.
1. La entrega se debe realizar mediante un repositorio git que incluya el código a entregar, y la documentación que se estime conveniente. Por lo tanto, el mail de entrega debería limitarse a consignar la URL del repositorio. Obviamente, el docente debe tener acceso a dicho repositorio, al menos de lectura.  
Se pide usar uno entre github, bitbucket o gitlab, que son los repositorios en los que este docente tiene cuenta.

<br/> 

## Elementos 
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
| `oxigeno.valencia()` | 4 |oxigeno.valenciaS)'C'`.numeroAtomico()| 6 8
| `oxigeno.valencia()` | 4 |oxigenN.7)opesoAtomico`14numeroAtomico()| 4 8
| `oxigeno.simbolo()` | "O" |

dado que `oxigeno.valencia()` ` es el carbono, y ``oxigeno.valencia()`` es el nitrógeno.

<br/>

Los tests deben incluir al oxígeno y al hidrógeno, teniendo en cuenta que el isótopo más usual del hidrógeno no tiene ningún neutrón, siendo 1 su peso atómico.

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

### Mejoras
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
¡OUO! lo que devuelva `elementosPresentes()` (lista, set o iterador) no puede tener repetidos.
* sobre enlaces: `cantEnlaces()`, `cantEnlacesAtomo(nombre)`, `conQuienesEstaEnlazado(nombre)`.
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
| `nh3.conQuienesEstaEnlazado("H2")]` | `["N1"]` |
| `nh3.conQuienesEstaEnlazado("N1")]` | `["H1", "H2", "H3"]` |
| `nh3.masaMolar()]` | 17 |
| `nh3.proporcionSobreMasa(tabla.elementoS('N'))]` | 0.8235 |

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

<br/>

**Sugerencia para lo que sigue**  
Definir variables correspondientes a compuestos comunes que puedan utilizarse en lo que sigue, p.ej. `agua`, `metano`, `nh3`, `co2`. Un ejemplo más voluminoso es la cisteina.


### Mejoras
Agregar los métodos `agregarAtomos` y `enlazarConVarios`, de forma tal que la creación de una molécula de amoníaco pueda reducirse a lo siguiente:
```
    nh3 = Compuesto('NH3')
    nh3.agregarAtomo(tabla.elementoS("N"), "N1")
    nh3.agregarAtomos(tabla.elementoS("H"), ["H2", "H3", "H4"])
    nh3.enlazarConVarios("N1", ["H2", "H3", "H4"])
```

Lograr que los nombres de átomo en una molécula se generen automáticamente. Esto nos permitiría llegar a una creación aún más compacta:
```
    nh3 = Compuesto('NH3')
    nh3.agregarAtomo(tabla.elementoS("N"))
    nh3.agregarAtomos(tabla.elementoS("H"), 3)
    nh3.enlazarConVarios("N1", ["H2", "H3", "H4"])
```

**Validación enlaces**  
Lograr que los compuestos soporten las siguientes operaciones: 
* `enlacesOK()`: indica si la definición de enlaces es correcta. Posibles causas para que no sea así: incluir, en un enlace, un nombre de átomo que no pertenece al compuesto (p.ej. en el amoníaco si hiciéramos `nh3.enlazar("N1", "C5")`); o que un átomo tenga más enlaces que su valencia (p.ej. si en lugar de enlazar N1 con H3, enlazáramos por error H2 con H3, entonces H2 tendría más enlaces que su valencia).
* `atomosConEnlacesSobrantes()`: devuelve la lista de átomos que tienen más enlaces que su valencia.
* `atomosConEnlacesDisponibles()`: devuelve la lista de átomos que tienen menos enlaces que su valencia, por lo que se pueden agregar enlaces en los que intervenga el átomo. P.ej. en el caso erróneo mencionado más arriba tendríamos `nh3.atomosConEnlacesDisponibles() = ['N1']`.

**Relación entre elementos**  
Lograr que los compuestos soporten las siguientes operaciones: 
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

Si se agrega a posteriori una cantidad de moles de un compuesto que ya está presente, entonces esta cantidad *se suma* a la que ya contiene. P.ej. si agregamos lo siguiente a la definición anterior:
```
medioRaro.agregarComponente(nh3, 15)
```
entonces este medio pasaría de 6 a 21 moles de amoníaco.

El modelo de un medio debe soportar las siguientes operaciones:
* `masaTotal()`, considerando la cantidad de moles de cada elemento.
* `elementosPresentes()`, considerando todos los compuestos involucrados. 
¡OUO! lo que devuelva (lista, set o iterador) no puede tener repetidos.
* `compuestosPresentes()`, también sin repetidos.
* `cantMolesElemento(elem)`, la cantidad total de moles del elemento indicado en el medio, considerando todos los compuestos incluidos y sus cantidades.
* `masaDeCompuesto(comp)` y `masaDeElemento(elem)`, los totales para el medio.
* `proporcionElementoSobreMasa(elem)` y `proporcionCompuestoSobreMasa(comp)`.

P.ej. en el medio definido tenemos:
* masa total: 3093 gramos.
* elementos presentes: hidrógeno, oxígeno, nitrógeno y carbono.
* compuestos presentes: agua, amoníaco, metano y dióxido de carbono.
* cantidad de moles de oxígeno: 128; de hidrógeno: 343.
* masa de agua: 1800 gramos; de amoníaco, 357 gramos.
* masa de oxígeno: 2048 gramos; de carbono: 408 gramos.
* proporción de agua sobre masa: 0.5819.
* proprción de oxígeno sobre masa: 0.6621; de hidrógeno: 0.1108.

<br/>

## Descripción textual de medio

```
descripcion = Descripcion("[H2O][CO2][H2O][CH4]")
```

apareceCompuesto(comp), molesCompuesto(comp), quienesAparecen(listaCompuestos).


### Agregados
compuestosDesconocidos(listaCompuesto), agregarAMedio(medio).

```
descripcion2 = DescripcionConCantidades("[H2O](1000)[CO2](50)[CH4](25)")
```

escalar(nro)

<br/>

## Reacciones químicas
Se definen a partir de insumos y productos.

reaccion.sePuedeAplicar(medio) # tiene todos los insumos
reaccion.aplicar(medio, proporcion)


















