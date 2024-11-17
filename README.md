# SHELL SRIPTING
1. Fundamentos
2. Programación
3. Programación Estructúrada
4. Programación de Tareas
5. Administración del Sistema
6. Depuración de Scripts

## 1. Fundamentos
> [!NOTE]  
> Antes de comenzar, se ha de puntualizar lo siguiente:
> - El Shell es un intérprete de comandos que permite ejecutar determinadas tareas.
> - El Shell de GNU/Linux incorpora sentencias de control de flujo, asignación, funciones, etc.
> - Los programas de Shell no necesitan ser complicados y son ejecutados línea a línea, de allí el nombre "Shell Scripts".
> - El significado de BASH es (Bourne Again Shell).

La **Shell** (_intérprete de comandos_), es la interfaz que nos permite interactuar con el sistema, siendo tanto una **interfaz de ejecucion de órdenes y utilidades como un lenguaje de programación** que permite _crear nuevas órdenes_ (**_shellscripts_**), utilizando combinaciones de comandos y estructuras lógicas de control.

> [!IMPORTANT]  
> El funcionamiento de la Shell:
> 1. Lee la línea de comando.
> 2. Interpreta su significado.
> 3. Efectua el comando.
> 4. Regresa el resultado por medio de las salidas.
> 
> Es simple, sencillo de entender e intuitivo, pero en ocasiones se suele olvidar.

![image](https://github.com/user-attachments/assets/67ccc413-bf22-4a7e-864a-73aec056ebe3)

- **Kernel**: Es el núcleo principal responsable de la ejecucion de tareas y de los servicios críticos del OS. Siendo el programa principal que interactua con todos los componentes del hardware y provee soporte para la ejecución de aplicacinoes.
- **Shell**: Es la encargada de permitirnos interactúar con el Kernel accediendo a los servicios provistos por el mismo a través de _System Calls_.

> [!NOTE]
> **System Call** (llamada al sistema): es un método utilizado por los programas de aplicación para comunicarse con el kernel del sistema. Siendo estas, el punto de enlace entre el modo usuario y el modo kernel.

### Tipos de Shell
Existen principalmente dos familias principales de intérpretes de comandos:
1. Los basados en Bourne: `SH`, `KSH`, `BASH` y `ZSH`.
2. Los basados en C: `CSH` o `TCSH`.

Para revisar los Shell de los que disponemos en un entorno Linux, se debe consultar el fichero `/etc/shells`:
```sh
> cat /etc/shells 

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

A cada usuario se le asigan un único Shell por defecto. Dicha asiganción se encuentra en el fichero `/etc/passwd`:
```txt
xpercival:x:1000:1000:xpercival,,,,:/home/xpercival:/bin/bash
```

### Shell del Sistema
Este es denóminado **_Login Shell_** y es la Shell por defecto que inicia UNIX y que se encargará de mostrar el indicador de órdenes de la sesión. Para conocer el Shell asignado, podemoste referirnos a la variable `$SHELL`, que contiene el valor de la Shell actual:
```sh
> echo $SHELL
/bin/bash
```

### Bash
Es el intérprete de comandos más utilizados e incluye un completo lenguaje de programacion estructurada y gran variedad de funciones internas. Sus principales características son:
- La ejecucion _síncrona_ (secuencial) de comandos o _asíncrona_ (paralela).
- Diferentes tipos de redirecciones de input/output para el control y filtrado de información.
- Control del entorno de los procesos.
- Ejecucion de comandos interactiva y desatendida, permitiendoosla entradas desde teclado, ficheros, etc.
- Aportación de una series de órdenes internas para la manipulación directa del intérprete y del entorno de la operacion.
- Incorporación de variables, operadores, estructuras de control de flujo, entrecomillados, sustituciones de valores y funciones.
- Control de trabajos en primer plano (_foreground_) y en segundo plano (_background_).
- Disposicion de un historial de comandos, creacionista de alias y disposición de una pila de directorios.

### Modos de Ejecucion de Comandos
> [!IMPORTANT]  
> Cuando un programa es ejecutado con Bash, se crea un nuevo proceso donde Bash hace una copia exacta de sí mismo. Este proceso hijo trabaja en el mismo entorno que su padre, y solo el Identificador (ID) de proceso es distinto. Este proceso es conocido como **Forking** (bifurcación).
> 
> Posterior al **Forking**, el espacio de direcciones del proceso hijo se sobrescribe con los datos del nuevo proceso mediante una llamada a `exec`.
>
> Este mecanismo `Fork-and-Exec` conmuta entre comandos, mientras que el entorno en el que se ejecuta el nuevo programa permanece inmutable, incluyendo la configuracion de los dispositivos de input/output, las variables de entorno y la prioridad.

#### Comandos Built-In

