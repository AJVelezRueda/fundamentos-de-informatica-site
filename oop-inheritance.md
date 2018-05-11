<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# POO - herencia
Python soporta la *herencia* de clases, una herramienta clásica que brinda la POO.

En la definición de una clase se puede indicar que **hereda**, o **extiende**, otra clase previamente definida. De esta forma, la nueva clase incorpora automáticamente todos los elementos (métodos y atributos) definidas en la clase de la que hereda, pudiendo agregar atributos y también refinar los métodos heredados.  
Veamos un ejemplo de una clase que extiende a la clase `Golondrina`, definida en la [página introductoria a la POO](./oop-intro.md).
```
class GolondrinaPensativa(Golondrina):
    def __init__(self):
        super().__init__()
        self._minutosQuePenso = 0

    def pensar(self, minutos):
        self._minutosQuePenso += minutos

    def minutosQuePenso(self):
        return self._minutosQuePenso

    def comer(self, gramos):
        super().comer(gramos)
        if (100 <= gramos <= 150):
            self.pensar(2)

    def estaEnEquilibrio(self):
        return super().estaEnEquilibrio() or (self._minutosQuePenso % 5 == 0)
```

Veamos varios detalles de la herencia a partir de cómo se reflejan en esta definición.
* Al agregar `(Golondrina)` a continuación del nombre de la clase, estamos indicando que la clase `GolondrinaPensativa` hereda de `Golondrina`, por lo tanto incorpora la definición del atributo `energiaActual` y los métodos `comer`, `volar`, `energia`, `estaDebil` y `estaEnEquilibrio`.
* El constructor tiene dos líneas. En la primera se invoca al constructor definido en la `super`clase, o sea en `Golondrina`. En la segunda se agrega un atributo, `_minutosQuePenso`, que queda definido en `GolondrinaPensativa`.
* Se agregan dos métodos, `pensar` y `minutosQuePenso`, que no están presentes en `Golondrina`.
* Se **redefine** el método `comer` que está presente en `Golondrina`. En la primer línea de ese método, se invoca a la versión del mismo método heredada de la clase `Golondrina`. Luego de eso, se hace un agregado que es válido solamente para las instancias de `GolondrinaPensativa`.
* En forma análoga, se redefine `estaEnEquilibrio`, combinando la condición heredada de `Golondrina` con un agregado propio de `GolondrinaPensativa`.

Definamos una instancia de `GolondrinaPensativa` y usémosla un poco:
```
>>> soraya = aves.GolondrinaPensativa()
>>> soraya.energia()
0
>>> soraya.minutosQuePenso()
0
```
Notamos que `soraya` acepta tanto las operaciones definidas en `GolondrinaPensativa` como las heredadas de `Golondrina`.

Veamos qué pasa con una operación redefinida:
```
>>> soraya.comer(120)
>>> soraya.energia()
480
>>> soraya.minutosQuePenso()
2
```
Podemos apreciar que se combinan los efectos heredados de `Golondrina` (en este caso, el aumento de la energía) con los agregados en `GolondrinaPensativa` (pensar dos minutos).

<br/>

**Nomenclatura**:  
Se usan los términos **superclase** y **subclase** para denotar que una clase (la subclase) hereda de otra (la superclase).
En el ejemplo, `GolondrinaPensativa` es subclase de `Golondrina`. Recíprocamente,  `Golondrina` es superclase de `GolondrinaPensativa`.

<br/>

## Template method
La herencia da lugar a una técnica usada comúnmente en POO, llamada *template method*. Para introducirla con un ejemplo, incorporemos esta definición de clase 
```
class Animal:
    def hacerCuidadoBasico(self):
        if (self.estaDebil()):
            self.comer(10)
```

y transformemos a `Golondrina` y `Perro` (esta última introducida en la [página de referencias](./oop-references.md)) en subclases de `Animal`:
```
class Golondrina(Animal):
  ...

class Perro(Animal):
  ...

```

Así las cosas, tanto `Golondrina` como `Perro` incorporan la definición del método `hacerCuidadoBasico`.
Este método define una estructura básica: si el animal está débil, se lo alimenta. Esta estructura es común a golondrinas y perros. Por otro lado, notamos que tanto el criterio para considerar que un animal está débil, como el efecto de alimentarse, son diferentes entre estas dos clases.  
Esta diferencia *no impide* que se pueda definir la estructura en la superclase. Cada subclase proporciona la definición específica de las piezas utilizadas en dicha estructura.

Esto funciona; si definimos
```
>>> ornella = oop.aves.Golondrina()
>>> lassie = oop.aves.Perro()
>>> jacinta = oop.aves.Golondrina()
>>> jacinta.comer(50)
>>> jacinta.energia()
200
```
podemos aplicar la operación heredada a golondrinas y perros:
```
>>> ornella.hacerCuidadoBasico()
>>> lassie.hacerCuidadoBasico()
>>> ornella.energia()
40
>>> lassie.energia()
10
>>> jacinta.hacerCuidadoBasico()
>>> jacinta.energia()
200
```
Jacinta no se ve afectada porque no estaba débil.
