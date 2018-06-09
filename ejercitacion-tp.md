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
Definir variables correspondientes a los elementos más usuales, p.ej. `oxigeno`, `hidrogeno`, etc., que puedan ser importadas en los tests de las etapas siguientes. También se puede tener una variable `tabla`, que referencie a una instancia de `TablaPeriodica` que tenga los elementos ya agregados.

### Mejoras
Que sólo agregue un elemento si no está ya en la lista, de acuerdo a su símbolo.

<br/>

## Moléculas
Desarrollar una clase `Molecula`. Una molécula se construye en dos fases: primero se agregan los átomos, y luego los enlaces.
Para cada átomo se indican: el elemento, y el nombre del átomo dentro de la molécula. Estos nombres se usan para definir los enlaces.

Este es un ejemplo, de la creación de una molécula de amoníaco:
```
    molecNh3 = Molecula()
    molecNh3.agregarAtomo(tabla.elementoS("N"), "N1")
    molecNh3.agregarAtomo(tabla.elementoS("H"), "H2")
    molecNh3.agregarAtomo(tabla.elementoS("H"), "H3")
    molecNh3.agregarAtomo(tabla.elementoS("H"), "H4")
    molecNh3.enlazar("N1", "H2")
    molecNh3.enlazar("N1", "H3")
    molecNh3.enlazar("N1", "H4")
```

**Atención**  
Se contemplan solamente enlaces covalentes.

El  modelo debe soportar estas operaciones: 
* sobre átomos y sus elementos: `cantAtomos()`, `atomosDe(elemento)`, `incluyeAtomo(nombre)`, `incluyeElemento(elemento)`, `elementosPresentes()`.
* sobre enlaces: `cantEnlaces()`, `cantEnlacesAtomo(nombre)`.
* otros: `masaMolar()`. 






### Mejoras
Agregar los métodos `agregarAtomos` y `enlazarConVarios`, de forma tal que la creación de una molécula de amoníaco pueda reducirse a lo siguiente:
```
    molec = Molecula()
    molec.agregarAtomo(tabla.elementoS("N"), "N1")
    molec.agregarAtomos(tabla.elementoS("H"), ["H2", "H3", "H4"])
    molec.enlazarConVarios("N1", ["H2", "H3", "H4"])
```

Lograr que los nombres de átomo en una molécula se generen automáticamente. Esto nos permitiría llegar a una creación aún más compacta:
```
    molec = Molecula()
    molec.agregarAtomo(tabla.elementoS("N"))
    molec.agregarAtomos(tabla.elementoS("H"), 3)
    molec.enlazarConVarios("N1", ["H2", "H3", "H4"])
```

Validación enlaces:






















