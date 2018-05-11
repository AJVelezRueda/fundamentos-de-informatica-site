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

Para 

