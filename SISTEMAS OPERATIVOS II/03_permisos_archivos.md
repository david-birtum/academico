# Permisos y atributos archivos

## Preliminar - Usuario root

El usuario root en GNU/Linux es el usuario que tiene privilegios de administrador en el sistema. Los usuarios "normales" no tienen estos privilegios por razones de seguridad. En algunas distribuciones no se encuentra disponible de forma predeterminada. En su lugar, se da acceso administrativo a usuarios individuales, que pueden utilizar la aplicación "sudo" para realizar tareas administrativas.

## Atributos de archivos y directorios

Los permisos de archivo UNIX tradicionales pueden asignar propiedad a tres clases de usuarios:

* **usuario**: El propietario del archivo o directorio, que, normalmente, es el usuario que creó el archivo. El propietario de un archivo puede decidir quién tiene derecho a leer el archivo, escribir en el archivo (realizar cambios en él) o, si el archivo es un comando; ejecutar el archivo.

* **grupo**: Los miembros de un grupo de usuarios.

* **otros**: Todos los demás usuarios que no son los propietarios del archivo y no son miembros del grupo.

Los usuarios o roles con capacidades administrativas, como root o el rol de administrador principal, pueden cambiar la propiedad de un archivo.

## Permisos de archivo UNIX

A continuación se muestran y se describen los permisos que puede otorgar a cada clase de usuario para un archivo o directorio.

* Lectura **r**
  * Los usuarios designados pueden abrir y leer el contenido de un archivo.
* Escritura **w**
  * Los usuarios designados pueden modificar el contenido del archivo o eliminar el archivo.
* Ejecución **x**
  * Los usuarios designados pueden ejecutar el archivo si es un programa o una secuencia de comandos de shell. También pueden ejecutar el programa con una de las llamadas del sistema.
* Denegado **-**
  * Los usuarios designados no pueden leer, escribir ni ejecutar el archivo.

## chmod

El programa de línea de comandos chmod, abreviatura de change mode (cambiar modo).
En los sistemas operativos tipo Unix multiusuario, chmod sirve para asignar permisos de acceso a archivos y directorios en sistemas de archivos compatibles con los permisos de archivo típicos de Unix.
Para hacer cualquier modificación en los atributos de los archivos chmod, es necesario ser propietario del archivo o contar con derechos root (administrador).

### ¿Cómo utilizarlo?

En Unix, el sistema de permisos de acceso a los archivos se basa en dos elementos fundamentales: las clases de usuario y los permisos básicos individuales. En la gestión de estos permisos, chmod soporta dos modos diferentes: la notación simbólica con letras (modo simbólico o carácter) y la atribución de permisos con códigos octales de cifras (modo octal), chmod sigue esta sintaxis:

``` $ chmod options mode file ```

Al comando chmod le sigue el elemento opcional *options*, que permite definir opciones avanzadas. El elemento mode representa el modo que se aplicará a file, que podrá ser un archivo o un directorio. El modo indica si una clase de usuario debe recibir permisos de acceso o si los permisos con los que cuenta se han de retirar.

### Modo simbólico o carácter

En el modo simbólico se asignan letras a las clases de usuarios y a los distintos permisos de acceso posibles. Combinándolos, puede definirse muy fácilmente qué derechos se han de otorgar o retirar y a qué usuarios, como se muestra a continuación:

* u -> user, propietario
* g - > group, grupo
* o -> other, otros
* a -> all, todas las clases

Si la definición de los derechos se hace por el modo simbólico, para vincular las clases de usuario con sus respectivos permisos se utilizan los siguientes operadores:

* Con el operador **+** se asignan más derechos de archivo a una clase de usuario. Solo se sobrescriben los derechos afectados.
* El operador **-** retira derechos de acceso a una clase de usuario.  
* Si los permisos de archivo de una clase de usuario se han de renovar, sin importar qué derechos tuvo antes, se usa el operador **=**.

#### Octal

Octal | Binario | Permisos de archivo
-- | -- | --
0 | 000 | —
1 | 001 | -x
2 | 010 | -w-
3 | 011 | -wx
4 | 100 | r-
5 | 101 | r-x
6 | 110 | rw-
7 | 111 | rwx
| |

Normalmente sólo tendrás que usar algunos muy comunes: 7(rwx), 6(rw-), 5(r-x), 4(r–), y 0(—).

```
$chmod 600 foo.txt 
-rw------- 1 me me 0 2020-03-06 14:52 foo.txt
 ```

#### Notación simbólica

chmod también soporta notación simbólica para especificar los permisos de archivo. La notación simbólica se divide en tres partes: a quién afecta el cambio, qué operaciónes se realizarán, y qué permisos se establecerán. Para especificar quién se ve afectado se usa una combinación de los caracteres “u”, “g”, “o” y “a” de la siguiente manera:

Octal | Significado
-- | --
u | Abreviatura de “usuario” pero significa el propietario del archivo o el directorio.
g | El grupo propietario
o | Abreviatura de “otros”, pero se refiere al mundo
a | Abreviatura de “all” (todos). Es la combinación de “u”, “g” y “o”
|

Si no se especifica ningún carácter, se asume “all”. La operación puede ser un “+” indicando que un permiso ha de ser añadido, un “-” indicando que un permiso ha de ser retirado, o un “=” indicando que sólo los permisos especificados deben ser aplicados y todos los demás han de ser eliminados.

Los permisos se especifican con los caracteres “r”, “w” y “x”. 

Notación | Significado
-- | --
u+x | Añade permisos de ejecución para el propietario.
u-x | Elimina permisos de ejecución del propietario
+x | Añade permisos de ejecución para el propietario, el grupo y el mundo. Equivalente a a+x
o-rw | Elimina los permisos de lectura y escritura para cualquier persona, que no sea el propietario ni el grupo propietario.
go=rw | Configura al grupo propietario y a cualquier persona, que no sea el propietario, para que tengan permisos de lectura y escritura. Si el grupo propietario o el mundo previamente tenían permisos de ejecución, los elimina.
u+x, go=rx | Añade permisos de ejecución para el propietario y establece los permisos para el grupo y para otros de lectura y ejecución. Múltiples especificaciones pueden ser separadas por comas.
|
```
$ chmod u+x,g+x foo.sh
-rwxrwxr-- 1 me me 263 agto 15 2020 foo.sh
 ```

Nota: Podemos indagar más información sobre el uso de comandos con man, en este caso $man chmod nos proporciona el manual de chmod.

Bibliografía:

  `https://www.ionos.mx/digitalguide/servidores/know-how/asignacion-de-permisos-de-acceso-con-chmod/`
  `https://help.ubuntu.com/kubuntu/desktopguide/es/root-and-sudo.html/`
  `https://patojad.com.ar/linux/2021/01/cambiando-los-permisos-de-un-archivo/`
