---
marp: false
---

# Kernel

El término proviene del aleman kern que signigica núcleo.
En nuestro contexto es el conjunto de elementos de software que se ejecutan en modo "administrador" (acceso seguro al hardware).

## El núcleo del Sistema Operativo

Como ya hemos discutido anteriormente, una de las tareas del Sistema Operativo es el control de los diferentes elementos de hardware, de la buena interacción que haya entre ambos, dependerá el óptimo funcionamiento de nuestro equipo informático.

El kernel entonces funge como intermediario entre el hardware y el software, el sistema operativo envía diversas solicitudes que el kernel procesa y envía a algún componente de hardware que se encargará de ejecutarlas en su nivel. A saber que en el kerner se cargan los controladores por lo tanto lo podemos considerar la parte del Sistema Operativo que se encarga de gestionar el hardware.

## Estructura

UNIX es un sistema operativo de tiempo compartido
(el sistema UNIX divide el tiempo de la computadora
en un número de partes, repartiéndose entre los
diferentes procesos).

El kernel del sistema es un programa que siempre
está residente en memoria y, entre otros, brinda los
siguientes servicios:

### El Kernel controla los recursos básicos

1. Controla los dispositivos periféricos (discos, terminales, impresoras, etc.).

2. Permite a distintos usuarios compartir recursos y ejecutar sus programas.

3. Proporciona un sistema de archivos que administra el almacenamiento de información (programas, datos, documentos, etc.).

4. Es un sistema interactivo, permite el redireccionamiento de la E/S, tuberías y ejecución de procesos en background Conceptos previos: proceso, estados de un proceso, servicio, uso de la memoria principal, llamadas al sistema.

### En un sentido más amplio, UNIX abarca también un conjunto de programas estándar

1. Compilador de lenguaje C (cc).
2. Editor de texto (vi).
3. Intérprete de órdenes (sh, ksh, csh, etc.).
4. Programas de gestión de archivos y directorios (cp, rm, mv, mkdir, rmdir, etc.).

### Organización de los Sistemas Unix

![kernel](https://lh3.googleusercontent.com/HDcDY3GBrK9ypFVkWSS9yLx2KSKP5jC8e3B2QtuNHmluwZxpXxKdap53ZIVYY0lrd5O-O-G9qMltmn67R1aBCqznppe6CPeOHhsmXdGZCMN2iXzsL_UzVMc1sRXBcvfQVPVxUuIVsQ=w2400)

1. Todas aquellas funciones que se necesitan inmediatamente, se mantienen permanentemente en memoria. A la parte residente en memoria de un sistema operativo se llama kernel. La mayoría de las funciones del Sistema Operativo las deben de proporcionar los programas de utilidad.

2.- Los programas estándar de cualquier sistema UNIX (vi, grep, sh, who, ...) y programas generados por el usuario. Estos programas nunca van a actuar sobre el hardware de forma directa. Por ello, debe de existir algún mecanismo que permita indicarle al kernel que necesitamos operar sobre algún recurso hardware. Este mecanismo es lo que se conoce como llamadas al sistema (system calls). Cualquier programa que se esté ejecutando bajo el control de UNIX, cuando necesite hacer uso de alguno de los recursos que le brinda el sistema, deberá efectuar una llamada a alguna de las llamadas al sistema (system calls).

3.- Aplicaciones que se sirven de otros programas ya creados para llevar a cabo su función. Estas aplicaciones, tampoco se comunican directamente con el kernel.
