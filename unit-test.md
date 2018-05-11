<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Testeo automático
Para probar cómo se comporta la biblioteca básica de Python, o para comprobar que algo que hicimos nosotros funciona correctamente, contamos con el REPL como herramienta. 

Un ejemplo sencillo: si queremos probar que el método `extend` de las listas funciona como pensamos, podemos hacer algo así:
```
>>> nums = [3,8,2,21,9]
>>> nums.extend([42,2,7])
>>> nums
[3,8,2,21,9,42,2,7]
```
y observar que el resultado coincide con el esperado.

Ahora, si queremos comprobar lo que nosotros hacemos, y ante cada cambio o agregado verificar que no rompimos nada, deberíamos ejecutar rutinariamente una batería de comprobaciones, y verificar que en cada una el resultado es el esperado.

Las herramientas de **testeo automatizado** son usadas para realizar este tipo de verificaciones en forma automática. 
Existen varias herramientas de este tipo en el ecosistema Python. En esta página vamos a usar `unittest`, que se integra bien con el IDE PyCharm.

</br>

Un test automatizado (usualmente conocido también como **test unitario**) es un programa cuyo objetivo es testear otro programa.

Las características básicas pueden verse a partir de un ejemplo sencillo:
```
import unittest

class PythonListTest(unittest.TestCase):
    def test_extend(self):
        nums = [3, 8, 2, 21, 9]
        nums.extend([42, 2, 7])
        self.assertEqual([3, 8, 2, 21, 9, 42, 2, 7], nums)

    def test_list_comprehension(self):
        nums = [3, 8, 2, 21, 9]
        self.assertEqual([3,21,9], [x for x in nums if x % 2 == 1])
```

Un test (más precisamente, un conjunto de tests) se define como una clase que hereda de la clase `TestCase`, que se importa del módulo `unittest`.

Una clase configurada de esta forma, define un test para cada método *cuyo nombre comience con `test`*. La clase puede incluir otros métodos, que no son considerados tests por la herramienta `unittest`.

En cada método incluimos el código con el que queremos trabajar. Para hacer una verificación, recurrimos a métodos que nuestra clase de test hereda de `TestCase`. 

El más sencillo de estos métodos es `assertEqual`. Recibe dos parámetros: 
* el primero es el *valor esperado*, o sea, el resultado que según nosotros debería obtenerse al evaluar la expresión.
* el segundo es el *valor obtenido*, o sea, la expresión que queremos testear.

En este ejemplo, la clase incluye dos tests, el primero verifica cómo queda una lista luego de aplicarle `extend`, el segundo verifica el resultado de una [list comprehension](./python-lists-strings).

<br/>

## Ejecución de tests
Una vez que codificamos la clase de test, podemos probarla por línea de comandos de esta forma: 
```
python -m unittest <nombre-de-archivo>.PythonListTest
```
Se obtiene esta salida
```
..
----------------------------------------------------------------------
Ran 2 tests in 0.001s

OK
```

<br/>
Cambiemos uno de los tests para que no resulte exitoso:
```
    def test_list_comprehension(self):
        nums = [3, 8, 2, 21, 9]
        self.assertEqual([3,9], [x for x in nums if x % 2 == 1])
```

Ahora
```
D:\carlos\pythonbasics>python -m unittest python_list_test.PythonListTest
.F
======================================================================
FAIL: test_list_comprehension (python_list_test.PythonListTest)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "D:\carlos\prog\python\pycharm-projects\just-start\basics\python_list_test.py", line 11, in test_list_comprehension
    self.assertEqual([3,9], [x for x in nums if x % 2 == 1])
AssertionError: Lists differ: [3, 9] != [3, 21, 9]

First differing element 1:
9
21

Second list contains 1 additional elements.
First extra element 2:
9

- [3, 9]
+ [3, 21, 9]
?     ++++


----------------------------------------------------------------------
Ran 2 tests in 0.002s

FAILED (failures=1)
```

Se dan varios datos de la falla: la línea con el `assert` que falla, los valores esperado y obtenido, un análisis de dónde se encontró la diferencia.

Abajo se indica la cantidad de tests y la cantidad de fallas. En este caso, tenemos un test que falló, y uno que anduvo bien.

<br/>

## Un ejemplo de test de código propio
Para terminar, incluyamos un test sencillo de la clase `Golondrina`, descripta en [la página inicial sobre POO](./oop-intro.md).

Transcribimos aquí la definición de la clase, que suponemos dentro de un archivo `aves.py`.
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

Este es un test sencillo sobre el comportamiento de una golondrina
```
import unittest
import aves

class GolondrinaTest(unittest.TestCase):
    def test_basicos(self):
        pepita = aves.Golondrina()
        pepita.comer(60)
        pepita.volar(30)
        self.assertEqual(200, pepita.energia())
        self.assertTrue(pepita.estaEnEquilibrio())
        self.assertFalse(pepita.estaDebil())
```

La estructura es la misma que vimos en el test sobre las listas de Python. La única diferencia es que el código del test se refiere a los elementos (en este caso la clase) construidos por nosotros. Obsérvese que el test está en un archivo separado, se hace `import` del archivo donde se define aquello que queremos testear.

Notamos el uso de `assertTrue` y `assertFalse`, dos nuevos métodos de verificación heredados de `TestCase`. 
Mencionemos también `assertAlmostEqual`, que se usa para verificaciones en la que están involucrados números con decimales.

