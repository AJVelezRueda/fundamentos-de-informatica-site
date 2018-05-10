<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Programación orientada a objetos (POO)
Es un estilo de programación muy ampliamente difundido en el ámbito del desarrollo de software. La mayor parte de los lenguajes de programación actuales ofrecen soporte para este estilo, o *paradigma*, de programación.

En particular, Python brinda la capacidad de definir nuestros objetos para aprovechar las características de la POO.
Los conceptos de este estilo de programación aparecen también al usar la biblioteca standard de Python, dado que muchas de las entidades con las que interactuamos, incluyendo listas, strings e incluso números, son objetos.

En lo que sigue, se hará una presentación suscinta de algunos de los aspectos relevantes de la POO, con foco en lo que utilizaremos en este curso.

<br/>

## Primer vistazo
La POO se caracteriza por la definición y manipulación de ciertas entidades a las que se llama *objetos*.
Cada objeto admite ser manipulado por medio de operaciones que se aplican sobre los mismos. Una operación puede, o no, llevar parámetros.

En Python, cuando hacemos p.ej. 
```
"pepita".upper()
```
estamos aplicando la operación `toUpper`, que no lleva parámetros, sobre el objeto `"pepita"`, que es un String. Los Strings (así como las listas y los números) pueden ser tratados como objetos en Python. 

En este caso
```
"pepita".index("i")
```
la operación requiere un parámetro.

La notación que se usa en Python para aplicar una operación sobre un objeto es 
```
objeto.operacion()
```
o
```
objeto.operacion(parametros)
```
si la operación lleva parámetros. 

<br/>

Nótese la diferencia con aplicar una función
```
funcion(parametros)
```
en la que no hay un objeto al que se le aplica la función.
Es cierto que para aplicar una función que está en un módulo que importamos, también usamos la "notación de puntos", p.ej. 
```
re.findall("X(.*?)Y", "alfaXbetaYgammadeltaXepsilonYeta")
```
Hay una diferencia fundamental entre este caso y aplicar una operación sobre un objeto. Cuando nos referimos a un módulo, estamos aplicando una *función*, que siempre va a tener el mismo comportamiento si se la invoca con los mismos parámetros. Si evaluamos la última expresión, el resultado va a ser siempre `['beta', 'epsilon']`. En cambio, el comportamiento de la aplicación de una operación sobre un objeto depende de qué objeto se trate, aunque sea la misma operación con los mismos parámetros. P.ej. la evaluación de cada una de estas expresiones
```
"pepita".index("i")
"aburrido".index("i")
"tomate".index("i")
```
va a tener distintos efectos.

<br/>

Cada objeto mantiene cierta información, la necesaria para resolver adecuadamente sus operaciones.
Los detalles sobre cómo cada objeto maneja la información que necesita, deberían ser mayormente opacos. La interacción con un objeto debería darse, en principio, únicamente por medio de las operaciones que el objeto establece al efecto.

<br/>

Muchos de los elementos que usamos en Python, en particular Strings, listas y números, pueden ser tratados como objetos. Ya vimos dos ejemplos con Strings, para las listas podemos mencionar
```
nums = [1,3,8,21,4,8,3]
nums.extend([8,24])
nums.count(8)
```
donde aplicamos las operaciones `extend` y `count` a la lista `nums`.

Por otro lado, algunas funcionalidades sobre los elementos básicos se acceden mediante funciones genéricas. P.ej. para obtener la longitud de la lista `nums`, evaluamos
```
len(nums)
```
y no
```
nums.len()
```
La lista de las funciones incluidas en la biblioteca básica de Python 3.6.5 está en [esta página](https://docs.python.org/3/library/functions.html).

En las siguientes secciones veremos cómo definir y usar objetos creados por nosotros.

<br/>

## Clases - definición y uso
En Python, las definición de objetos se hace, principalmente, por medio de *clases*.
Una clase es un molde a partir del cual se pueden crear objetos que respondan a ciertas operaciones. 

<!-- En la siguiente, la usaremos para crear objetos y operar con ell -->

Tomemos como ejemplo un modelo trivial del comportamiento de una especie animal. Un ornitólogo propone un modelo acerca de cómo manejan la energía las golondrinas. En este momento, una golondrina tiene una cantidad de energía disponible, y hay solamente dos acciones que modifican esta cantidad: comer aumenta la energía disponible, mientras que volar la disminuye. 
Las variaciones propuestas son:
* cuando una golondrina come una cantidad X de gramos (digamos de alpiste, que es el único alimento que se tiene en cuenta en este modelo), su energía aumenta en X * 4.
* cuando una golondrina vuela X kilómetros, su energía disminuye en X - 10.
Adicionalmente, una golondrina se considera *débil* si su energía es menor a 100 unidades, y que está *en equilibrio* si este valor está entre 150 y 300.

<br/>

El modelo recién definido se puede plasmar en la siguiente definición en Python
```
class Golondrina:
    def __init__(self):
        self.energiaActual = 0

    def comer(self, gramos):
        self.energiaActual += 4 * gramos

    def volar(self, kms):
        self.energiaActual -= 10 + kms

    def energia(self):
        return self.energiaActual

    def estaDebil(self):
        return self.energia() < 100

    def estaEnEquilibrio(self):
        return 150 <= self.energia() <= 300
```

Se está definiendo una **clase** llamada `Golondrina`. 
Los objetos que se creen a partir de esta clase admitirán cinco operaciones: `comer`, `volar`, `energia`, `estaDebil`, y `estaEnEquilibrio`.
Para poder responder a estas operaciones, cada objeto que se cree a partir de esta clase deberá manejar un dato numérico, que es el valor de la energía de(l modelo de) la golondrina en ese momento. Ese valor se almacena en `self.energiaActual`.
La definición adicional `__init__` le da el valor inicial a esta variable.

Notamos que de las cinco operaciones, hay dos que modifican la información que maneja el objeto, a saber `comer` y `volar`.

Los objetos que se crean a partir de una clase se conocen como *instancias*  de esa clase.

<br/>

Supongamos que incluimos esta definición en un archivo llamado `aves.py`.  Evaluando esto en el REPL:
```
>>> import aves
>>> pepita = aves.Golondrina()
>>> juanita = aves.Golondrina()
```
creamos dos instancias de (la clase) `Golondrina`.

Al principio, las dos golondrinas tienen el mismo comportamiento
```
>>> pepita.energia()
0
>>> pepita.estaDebil()
True
>>> pepita.estaEnEquilibrio()
False
>>> juanita.energia()
0
>>> juanita.estaDebil()
True
>>> juanita.estaEnEquilibrio()
False
```

Ahora "démosle de comer" a una de ellas.
```
>>> pepita.comer(60)
```

Esto modifica la información de `pepita`, pero no la de `juanita`. Podemos ver las consecuencias en las otras operaciones
```
>>> pepita.energia()
240
>>> pepita.estaDebil()
False
>>> pepita.estaEnEquilibrio()
True
>>> juanita.energia()
0
>>> juanita.estaDebil()
True
>>> juanita.estaEnEquilibrio()
False
```

<br/>

Finalmente, en este caso
```
>>> pepita.peso()
Traceback (most recent call last):
  File "<input>", line 1, in <module>
AttributeError: 'Golondrina' object has no attribute 'peso'
```
el error indica que las instancias de `Golondrina` sólo responden a las definiciones incluidas en esa clase.

<br/>

## Algunas definiciones
A partir de la introducción informal de la sección anterior, definamos algunos conceptos.

La definición de una clase incluye **métodos** y **atributos** (o **variables de instancia**). 
Los métodos corresponden a las operaciones que quedan habilitadas para las instancias. Los atributos conforman la información que mantiene *cada instancia*. 

Cada método se define mediante un `def` dentro de la definición de la clase. La sintaxis es similar a la definición de una función, con la siguiente diferencia muy relevante.
El primer elemento en la lista de parámetros de un método, llamado `self`, es una referencia a la instancia sobre la que se aplica la operación correspondiente. 
P.ej. al evaluar `pepita.comer(60)`, `self` será `pepita`, mientras que de evaluarse p.ej. `juanita.comer(60)`, `self` será `juanita`.
Es por esto que evaluando `pepita.comer(60)` se modifica la `energiaActual` de `pepita`, no así la de `juanita`.

Los atributos se definen implícitamente, incluyendo `self.<nombre_de_atributo>` en los métodos. La clase `Golondrina` define un solo atributo, `energiaActual`.
El conjunto de atributos de un objeto, o sea la información que mantiene el objeto, se conoce como su *estado*.

El método especial `__init__` se evalúa inmediatamente después de crearse cada instancia. Por eso es un lugar ideal para dar valor inicial a los atributos.

<br/>

Finalmente, digamos que lo que en este texto se denomina "aplicar una operación sobre un objeto", en la literatura se conoce como "ejecutar/evaluar/invocar un método", o (menos frecuentemente) "enviar un mensaje".  
Este redactor prefiere dejar clara la distinción entre operación y método. El método es el código, está en la clase. La operación (o "mensaje") se aplica sobre (envía a) un objeto. 

Sobre esto un detalle importante: las operaciones que se definen en una clase no son para aplicar sobre ella, sino sobre sus instancias. P.ej.:
```
>>> aves.Golondrina.energia()
Traceback (most recent call last):
  File "<input>", line 1, in <module>
TypeError: energia() missing 1 required positional argument: 'self'
```
o sea, aplicar `energia` sobe *la clase* Golondrina resulta en un error.

<br/>

## Quién es `self`
Analicemos en particular este método:
```
    def estaDebil(self):
        return self.energia() < 100
```
Aquí se hace referencia a un objeto `self`, del que se está invocando la operación `energia`. 

En Python, `self` es un nombre especial para identificar al objeto sobre el que se hace una operación. P.ej. si evaluamos
```
pepita.estaDebil()
```
`self` va a ser `pepita`, y por lo tanto la evaluación se hace sobre la energía de esa golondrina.






