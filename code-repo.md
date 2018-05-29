<style>
.page-header {
    padding-bottom: 50px;
    padding-top: 50px;
}
</style>

[volver al inicio](./index.md)  

# Repositorios de código
Llamemos *repositorio* a cualquier herramienta que permita almacenar información, de forma tal que pueda ser accedida desde distintos equipos, idealmente mediante Internet.  
P.ej. Dropbox es un repositorio de documentos.   
Nótese que la funcionalidad principal de un repositorio es el almacenamiento, no la edición ni el despliegue. Ergo, en esta caracterización no entran p.ej. ni Google Drive ni Instagram.

En el ámbito del desarrollo de software, ya es standard almacenar el código en repositorios remotos específicos, que incluyen funcionalidades que resultan muy prácticas para manejar código fuente.  
En particular, estos repositorios están preparados para proyectos de desarrollo de software en los que trabajan muchos desarrolladores, dando herramientas que ayudan a consolidar el trabajo de todos ellos.

Los repositorios responden a distintas especificaciones. La más usada hoy en día es [**Git**](https://git-scm.com/).

<br/>

Una particularidad de Git es que existen varios sitios que permiten crear repositorios en forma gratuita. Mencionamos:
* [GitHub](https://github.com).
Es el más popular. Permite armar fácilmente sitios de documentación ... como este que estás leyendo.
* [GitLab](https://about.gitlab.com/).
Permite repositorios de uso privado asociados a cuentas gratuitas, lo que no es contemplado por ninguno de los otros.
* [BitBucket](https://bitbucket.org/).

<br/>

## Ideas básicas de Git
Por razones que escapan al alcance de esta introducción, Git define dos niveles de repositorio: el remoto (que está en un servidor al que se accede por Internet) y el local (que está en nuestra computadora).

Esto define tres espacios:
* el *espacio de trabajo*, o sea, la carpeta desde donde se editan los archivos.
* el *repositorio local*.
* el *repositorio remoto*.
El espacio de trabajo refleja la organización de los repositorios en carpetas anidadas.

Es importante tener en cuenta esto para entender que un archivo en mi espacio de trabajo debe pasar por **dos** etapas para llegar a un repositorio remoto.

<br/>

Los otros conceptos centrales en Git son **branch** y **commit**.
* Un branch es una línea de trabajo.  
Todo repositorio tiene una línea central que por lo general se conoce como *master*. A partir de ella, se pueden definir líneas separadas, que eventualmente pueden consolidarse.
* Un commit es una "foto" del estado de un repositorio Git en un momento determinado, que incluye el registro de los cambios desde el anterior commit en la misma rama. Un mismo commit puede formar parte de distintos branches.

<br/>

Ver las referencias más abajo para ejemplos y explicaciones adicionales de estos conceptos.

<br/>

## Para seguir leyendo

[Serie de tutoriales de Git](https://www.atlassian.com/git/tutorials)  
De los varios materiales que miré en su momento, es el que me resultó más claro.

[Apunte usado en la UNQ](https://web-ciu-programacion.github.io/site/material/documentos/apuntes/git-pequenia-introduccion-practica.pdf).  
Muy básico y tal vez podría mejorarse. Introducción paso-a-paso para adquirir la experticia básica que permita comenzar a usar Git en proyectos propios.

<br/>

## Comentario final
Git "es un mundo", tiene muchos comandos, que permiten manejos muy sutiles de la base de código.  
Para la mayor parte de los proyectos es suficiente manejarse a partir de una visión sencilla de Git, limitada a los comandos utilizados más habitualmente.



