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


## Aves y ornitólogos
Realizar una implementación del ejercicio 4 de la guía 5 en [la página de programación con objetos 1 de la UNQ](https://objetos1wollokunq.gitlab.io/material/#guides), el de atención de animales.

Luego, implementar el ejercicio 1 de la guía 7 del mismo sitio, que plantea agregados al mismo dominio.

