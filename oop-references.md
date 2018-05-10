<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# POO - varios objetos
En esta página continuamos explorando la POO, analizando qué pasa cuando entran varios objetos en escena.

## Referencias
Seguimos trabajando en base a la clase `Golondrina` definida en [la página introductoria sobre POO](./oop-intro.md).

Agreguemos la siguiente clase:
```
class Chico:
    def darMascota(self, unaMascota):
        self._mascota = unaMascota

    def mascota(self):
        return self._mascota

    def seSienteBien(self):
        return self.mascota().estaEnEquilibrio()

    def alimentarMascota(self):
        self.mascota().comer(50)
```
también en el archivo `aves.py`. En el REPL podemos crear una instancia, y asignarle una mascota
```
>>> roque = oop.aves.Chico()
>>> roque.darMascota(juanita)
```

Ahora el estado de `roque` consiste de una referencia *a una golondrina*, que puede obtenerse mediante la operación `mascota`. 
Supongamos que nunca le dimos de comer, ni hicimos volar, a `juanita`, por lo tanto su energía es 0. Por lo tanto, podemos hacer:
```
>>> juanita.energia()
0
>>> roque.mascota().energia()
0
```
Aquí se aplicaron *dos* operaciones, en orden:
* primero se aplicó `mascota` sobre `roque`. El *resultado* de esto es la instancia de `Golondrina` que conocemos como `juanita`.
* Al objeto *que resulta de la evaluación anterior* se le aplica `energia`, obteniéndose el resultado final `0`.

Si ahora le pedimos a `roque` que alimente a su mascota
```
>>> roque.alimentarMascota()
```
la golondrina que está siendo alimentada *es la que llamamos `juanita`*. Por lo tanto, ahora tenemos
```
>>> juanita.energia()
200
>>> roque.mascota().energia()
200
```
Ergo, hay un mismo objeto que tiene dos referencias, una es `juanita`, la otra es desde el estado de `roque`.

<br/>

## Objetos "anónimos"
Siguiendo con el ejemplo, ¿qué pasa si hacemos esto?
```
>>> roque.darMascota(aves.Golondrina())
```

Recordando que el código se evalúa de adentro hacia afuera, notamos que están pasando dos cosas: 
* se crea una nueva instancia de `Golondrina`
* ese nuevo objeto se asigna como mascota de `roque`

En este momento tenemos *tres* golondrinas en juego, a saber: `pepita`, `juanita`, y la mascota de `roque` que es una tercer golondrina, distinta a las otras dos. 
Verifiquemos la energía de cada una (recordando que en la página anterior le habíamos dado de comer 60 a `pepita`).
```
>>> pepita.energia()
240
>>> juanita.energia()
200
>>> roque.mascota().energia()
0
```

Veamos qué pasa después de que `juanita` vuela y `roque` alimenta:
```
>>> juanita.volar(20)
>>> roque.alimentarMascota()
>>> pepita.energia()
240
>>> juanita.energia()
170
>>> roque.mascota().energia()
200
```

<br/>

Pregunta para probar y pensar: ¿qué pasa si hacemos lo siguiente?:
```
>>> enriqueta = roque.mascota()
```
¿Se está creando una nueva golondrina, tenemos cuatro ahora? ¿Qué obtengo como resultado si le pido la energía a `enriqueta`?

<br/>

## Polimorfismo
Agregamos una tercer clase a nuestro modelo:
```
class Perro:
    def __init__(self):
        self._alimento = 0
        self._caricias = 0

    def energia(self):
        return self._alimento + (self._caricias * 10)

    def comer(self, gramos):
        self._alimento += gramos

    def acariciar(self):
        self._caricias += 1
```

Con esto, podemos crear un perro y dárselo a Roque como mascota
```
>>> fido = oop.aves.Perro()
>>> roque.darMascota(fido)
```

En este escenario, pensemos qué pasa si evaluamos
```
>>> fido = oop.aves.Perro()
>>> roque.alimentarMascota()
```

Preguntas: esto ¿anda o no anda? Si funciona, ¿tiene el efecto esperado?

<br/>

La respuesta a las dos preguntas es **sí**. El estado de `fido` se ve afectado:
```
>>> fido.energia()
50
```

Entonces, una golondrina sirve como mascota de un chico, y un perro también. ¿Cómo es que funciona esto, qué límites tiene?

<br/>

La respuesta se puede obtener a partir de mirar este método en `Chico`: 
```
    def alimentarMascota(self):
        self.mascota().comer(50)
```

Esta es la única operación, dentro del código de la clase `Chico`, que aplica una operación sobre su mascota.

Por lo tanto, **cualquier** objeto que soporte la operación `comer` con un parámetro numérico, puede funcionar como mascota de un chico. 
Esto incluye instancias de clases que se crean *después* de la clase `Chico`.

<br/>

Esta flexibilidad para combinar objetos refleja un fenómeno conocido como **polimorfismo**. En este caso, las golondrinas y los perros son polimórficos, porque soportan la misma operación (comer), y por lo tanto, en cualquier contexto donde se requiera solamente esa operación, puede utilizarse una golondrina o un perro indistintamente.

El nombre *polimorfismo* se refiere específicamente a que golondrinas y perros realizan la misma operación con distintos métodos, o sea, de distinta forma.

