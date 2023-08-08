**¿Que es el Event Loop?** (Single thread)
Es la tarea del SO que verifica que una tarea del proceso se ejecute y no termine hasta que se cumplan tres condiciones, 0 tareas de tiempo (setTimeout, setInterval, setInmediate), 0 tareas del sistema (escuchar puertos de un servidor), 0 tareas de procesamiento lento (leer archivos, leer información de un disco).

Estas comprobaciones se realizan en cada 'tick'  ademas de:
* Comprobar si alguna función de tiempo  esta lista para ser llamada.
* Comprobar si las tareas del sistema o de procesamiento llaman algún callback (por ejemplo si ya se termino de leer un archivo).
* Pausar la ejecución y continuar cuando una tarea haya sido completada.
* Verificar si una función de tiempo ejecuta una función inmediata.
* Handle any close events

**Threadpools**
Por su traducción en ingles, significa, piscina de hilos, eso quiere decir que este objeto contiene los diferentes hilos que se pueden ejecutar, todo depende de tu computador, sin embargo, en este caso, al realizase cinco tareas diferentes, cuatro de estas se asignan a cuatro hilos dentro de la piscina y a su vez estos se dirigen a los núcleos para ser ejecutada, una vex ejecutada, la quinta tarea se asignara y finalizara por separado.

Con esa variable de entorno 'process.env.UV_THREADSPOOL_SIZE = 2' se puede manipular la cantidad de hilos que se crean por piscina.

**OS Operations** (Async)
Para ser mas precisos, algunas tareas no se ejecutan en el motor v8, ni tampoco en el libuv, de hecho las peticiones https las realiza el sistema operativo, solo que pasan a travez de libuv y este esta pendiente de su finalización.

**Multithreads** (4 hilos por defecto)
De hecho se utilizaran miltiples hilos para realizar tareas que hagan uso de ellos, por ejemplo, haces hash de una cadena o leer el disco duro, sin embargo, si se realiza una tarea de http esta no hara uso de de los hilos y se ejecutara asincronamente.

Esto también incluye el hecho de que si una tarea hace uso de el disco externo esta tarea se pone en pausa mientras el disco externo ejecuta su proceso, otra tarea puede ser ejecutada en el hilo y cuando esta se reanude vovlera a un hilo disponible.

**Node performance**
Cruster Mode // Recommended

Worker Threads // Experimental



