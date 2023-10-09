# AdM

Arquitectura de microcontroladores

Alumno: Jesus Eduardo Gonzales Davila

# Preguntas orientadoras
## 1. Describa brevemente los diferentes perfiles de familias de microprocesadores/microcontroladores de ARM. Explique alguna de sus diferencias características.
La empresa ARM se dedica a desarrollar arquitecturas de microcontroladores para diferentes usos e industrias. A pesar de contar con varias familias a través de los años, desde sus origenes, en la actualidad la familia de microcontroladores con mayor uso es la familia Cortex. Dentro de esta familia tenemos variantes, como se aprecia en la imagen inferior. Para satisfacer las diferentes necesidades de aplicaciones se dividen en 3.
![image](https://github.com/jegd/AdM/assets/105693319/8863d09a-ecf2-4c44-876d-e8897fe7b01c)
- Cortex-A: Microcontrolares para sistemas que necesiten un alto desempeño. La mayoria en la página de ARM utiliza la arquitectura ARMv9. Frecuentemente se usa con Linux.
- Cortex-M: Microcontroladores utilizados para aplicaciones que requieren pequeños usos de energía. Encontramos aquí los microcontroladores Cortex-M0, Cortex-M0+, Cotex-M1, Cortex-M3 y Cortex-M4 que utilizan mayormente la arquitectura ARMv7 y ARMv6.
- Cortex-R: Son microcontroladores robustos con muy buen desempeño en procesamiento en tiempo real. Suelen usarse en la industria automotriz.
# Cortex M
## 1. Describa brevemente las diferencias entre las familias de procesadores Cortex M0, M3 y M4.
- Los microcontroladores Cortex-M3 y Cortex-M4 son microcontroladores que utilizan la arquitectura ARMv7. Ambos son microncontroladores de alto desempeño. Sin embargo algunos microcontroladores Cortex-M4 tienen añadidos que los Cortex-M3 no tienen como por ejemplo SIMD (Single instruction, multiple data), fast MAC e intrucciones de saturación aritmética, por lo que pueden ser utilizados en procesamiento de señales.
- Los microcontroladores Cortex-M0, Cortex-M0+ y Cortex-M1 son microcontroladores basados en al arquitectura ARMv6 que tienen un set de instrucciones más pequeño. Los Cortex-M0 y Cortex-M0+ son muy pequeños en tamaño. Los Cortex-M0+ tienen la mejor optimización de baja energía. Los microcontroladores Cortex-M1 son diseñados específicamente para aplicaiones de FPGA.
## 2. ¿Por qué se dice que el set de instrucciones Thumb permite mayor densidad de código? Explique
El set de instrucciones Thumb-2, que es el usado por los microcontroladores Cortex-M se dice que permite escribir código de alta densidad debido a que este set de isntrucciones combina la posibilidad de usar instrucciones tanto de 16 como 32 bits, sin cambiar de estado del set de instrucciones Thumb (16 bits) y el set ARM (32 bits). Cuando se compila se utiliza las intrucciones de 32 bits en medida de lo posible, sin embargo si no es posible se usarán las de 32 bits.
## 3. ¿Qué entiende por arquitectura load-store? ¿Qué tipo de instrucciones no posee este tipo de arquitectura?
La arquitectura Load-store, es un tipo de arquitectura de instrucciones en el que para acceder a un valor en un lugar de la memoria, debemos cargar el valor de esta dirección de memoria en un registro y de allí trabajarlo. No podemos trabjar directamente en el valor de la memoria. 
## 4. ¿Cómo es el mapa de memoria de la familia?
Los Cortex-M0, Cortex-M0+ y Cortex-M1 tienen una arquitectura de memoria Von Neumman mientras que los Cortex-M3, Cortex-M4 y Cortex-M7 tienen una arquitectura Hardvard. Tiene un mapa de memoria plano de 4GB donde las últimas direcciones ya están fijadas a ciertos periféricos internos y componentes de debug. A pesar de poder guardar y ejercutar código desde los espacios de memoria para SRAM y RAM, el procesador no está optimizado para esto.
![image](https://github.com/jegd/AdM/assets/105693319/25b127f0-551f-4622-832f-58b771e3ffca)
En la imagen superior extraída del libro base del curso, podemos observar como las direcciones de memoria tiene 32 bits y a partir de la dirección 0xE0000000 la memoria ya está fijada a componentes del mismo procesador.
## 5. ¿Qué ventajas presenta el uso de los “shadowed pointers” del PSP y el MSP?
El uso de un shadowed pointer permite separar el stack pointer del sistema operativo del stack pointer de la tarea (Process Stack Pointer PSP). Esto se aprecia en su aplicación en sistemas operativos. Cuando se trabaja en uso privilegiado se utiliza el Main Stack Pointer MSP. Esta independencia de los stack pointer permite proteger el programa para que no se modifique por error el stack pointer en el sistema operativo.
## 6. Describa los diferentes modos de privilegio y operación del Cortex M, sus relaciones y como se conmuta de uno al otro. Describa un ejemplo en el que se pasa del modo privilegiado a no priviligiado y nuevamente a privilegiado.
En los Cortex-M se tiene el modo privilegiado y el modo no proviliegiado para evitar que procesos no confiables de la apliacación arruinen el sistema. Un programa de modo no privilegiado no puede pasar por sí mismo al modo privilegiado. El programa empieza en modo privilegiado por defecto.
![image](https://github.com/jegd/AdM/assets/105693319/e6b3e2d4-26e9-497c-9ed7-958b3f4035ea)
En la imagen superior tenemos un ejemplo de una aplicación que inicia en modo provilegiado, después cambia al modo no privilegiado por medio del registro de control. Una vez en el modo no privilegiado, sólo se puede pasar cambiar al modo handler que es privilegiado, ocasianado por una excepción o interrupción. Para poder salir del modo no privilegiado es necesario entrar al modo handler y allí editar el registro de control. Estos modos de funcionamiento se aprecian en los sistemas operativos.
## 7. ¿Qué se entiende por modelo de registros ortogonal? Dé un ejemplo
Significa que se puede modificar un bit de un registro, sin que el cambio de uno influya en el otro. Un ejemplo de esto es el registro de control de Cortex-M en el que se pueden modificar los bits de SPSEL y nPRIV
![image](https://github.com/jegd/AdM/assets/105693319/a9e97ec8-331e-492a-996e-f1472ddf6b8f)
## 8. ¿Qué ventajas presenta el uso de intrucciones de ejecución condicional (IT)? Dé un ejemplo
La ventaja es que al utilización de estas instrucciones condiciones no destruye el pipeline. En Cortex-M podemos ejecutar hasta 4 instrucciones condiciones. Un ejemplo de 2 instrucciones condicionales es el siguiente:
ITE GE
ADDGE R0,R0,R1
ADDLT R0,R0,R2
## 9. Describa brevemente las excepciones más prioritarias (reset, NMI, Hardfault).
Reset: es la excepción más prioritaria, con una prioridad de (-3) que no es editable. 
NMI: excepción con el valor de prioridad de (-2), no es editable, Interrupción no enmascarable que puede ser generada por los periféricos del chip o por recursos externos.
HardFault: excepción con prioridad de (-1), no es editable, corresponde a todas las condiciones de fallo si es que el handler para estos fallos no está habilitado.
## 10. Describa las funciones principales de la pila. ¿Cómo resuelve la arquitectura el llamado a funciones y su retorno?
Cuando se produce un cambio de entorno se coloca en la pila los datos e información que se están utilizando en la función anctual, para luego pasar a la ejecución en otro entorno. Al momento de regresar al primer entorno se busca el valor del stack donde se indica la dirección de la función.
## 11. Describa la secuencia de reset del microprocesador.
Es la primera excepción que ejecuta el microcontrolador. La secuencia de reset primero carga la posición de memoria 0x000000 que es el valor del inicial del MSP y después de carga el valor del vector de reset que tiene posición máxima del stack pointer del programa.
![image](https://github.com/jegd/AdM/assets/105693319/6f684f8d-be18-4c61-a680-3cf5cac364ec)
## 12. ¿Qué entiende por “core peripherals”? ¿Qué diferencia existe entre estos y el resto de los periféricos?
Los core peripherals son los periféricos incluidos en el procesador. Tendrásn más prioridad que las interrupciones generadas por periféricos del microcontrolador externos al core.
![image](https://github.com/jegd/AdM/assets/105693319/78026511-ef37-4cba-b295-2b6b79b92a8d)
## 13. ¿Cómo se implementan las prioridades de las interrupciones? Dé un ejemplo
Las prioridades de las interrupciones están desginadas en el NVIC (Nested Vector Interrupt Controller) Vector controlador de interrupciones anidadas. 
![image](https://github.com/jegd/AdM/assets/105693319/e684559e-afc8-4d99-8d55-3c3638ed6106)
Se puede acceder a este en el archivo config.h donde se puede establecer un handler para una interrupción.
Un ejemplo de esto sería el Systick que tiene una prioridad editable.
## 14. ¿Qué es el CMSIS? ¿Qué función cumple? ¿Quién lo provee? ¿Qué ventajas aporta?
El CMSIS es "ARM Cortex Microcontroller Software Interface Standard” que es la capa de abstracción de hardware independiente del fabricante del microcontrolador. Son librerías escritas en C provistas por el propio ARM. Su objetivo es dar portabilidad entre microcontroladores Cortex-M.
## 15. Cuando ocurre una interrupción, asumiendo que está habilitada ¿Cómo opera el microprocesador para atender a la subrutina correspondiente? Explique con un ejemplo
Lo que ocurre cuando se presenta una interrupción es que se guarda el punto donde se quedó la ejecución  datos importantes. Imagen del stacking en tail chaining.
![image](https://github.com/jegd/AdM/assets/105693319/17ee4846-1267-4941-8d5e-6c37b22c90c2)
Un ejemplo lo podemos encontrar abajo donde se está en un modo no privilegiado, se pasa al modo handler, se ejecuta el handler correspondiente al Systick y finalmente se vuelve al entorno no privilegiado con información que se saca del stack.
![image](https://github.com/jegd/AdM/assets/105693319/704f3b00-1c5b-46b2-922a-30f02aaf25e5)
## 17. ¿Cómo cambia la operación de stacking al utilizar la unidad de punto flotante?
El stacking guarda los primeros 16 registros de la FPU más los estados de los flags por lo que se ocupa más memoria y además se toma más tiempo.
## 16. Explique las características avanzadas de atención a interrupciones: tail chaining y late arrival.
El modo de atención de tail chaining ocurre cuando se presenta una interrupción y se pasa al modo handler y cuando se está en este contexto se produce otra interrupción de menor o igual prioridad. Cuando se termina la interrupción se pasa a ejecutar la siguiente ejecución de menor o igual prioridad, pero en este caso no se da un cambio de contexto por lo que no se produce ningún stacking, y finalizando esta segunda interrupción se realiza recién el unstacking.
La atención late arrival se produce cuando se está haciendo el stacking y llega una interrupción de mayor prioridad que la interrupción que se iba atender. Se termina de realizar el stacking pero se atiende la interrupción de mayor prioridad para luego anteder a la de menor prioridad y terminar el unstacking.
## 17. ¿Qué es el systick? ¿Por qué puede afirmarse que su implementación favorece la portabilidad de los sistemas operativos embebidos?
El sysctick es un temporizador de 24 bits que se encuentra integrado en el núcleo del procesador. Se utiliza en los sistemas operativos de sistemas embebidos como time-slicer o sepador de tiempo por el scheduler que luego delega al pendSV el cambio de contexto para realizar la función que se tenga planificada.
## 18. ¿Qué funciones cumple la unidad de protección de memoria (MPU)?
La MPU significa Memory Protection Unit que genera hasta 8 regiones de memoria protegidas que no pueden ser accedidas por funciones que estén ejecutándose en el modo no privilegiado. También se puede utilizar para que aplicaciones accedan a periféricos sin los permisos adecuados. También por ejemplo para evitar que se ejecute código de zonas no deseadas como por ejemplo desde la RAM.
## 19. ¿Cuántas regiones pueden configurarse como máximo? ¿Qué ocurre en caso de haber solapamientos de las regiones? ¿Qué ocurre con las zonas de memoria no cubiertas por las regiones definidas?
Se puedene configurar un máximo de 8 regiones de memoria protegidas por el MPU. Si las zonas están zolapadas y habilitadas se tomarán las reglas de la zona más alta. Si la zona solapada está deshabilitada la región de memoria tendrás las mismas reglas de acceso que la región a la que se solapa. Cuando la zona de memoria no está solapada y está deshabilitada, intentar acceder a esta zona de memoria activará un MemManage Fault.
## 20. ¿Para qué se suele utilizar la excepción PendSV? ¿Cómo se relaciona su uso con el resto de las excepciones? Dé un ejemplo
Es una excepción que se llama en el modo handler para realizar el cambio de contexto en los sistemas operativos.
![image](https://github.com/jegd/AdM/assets/105693319/ff1e77b3-53c7-4f8a-a253-560af6f56768)
En el ejemplo de la imagen superior podemos ver cómo se pasa a ejecutar el handler del sysctick y finalizando para relaizar el cambio de contexto se pasa a utilizar la excepción PendSV para realizar el cambio de contexto y volver a ejecutar las funciones en el modo no privilegiado.
## 21. ¿Para qué se suele utilizar la excepción SVC? Expliquelo dentro de un marco de un sistema operativo embebido.
La excepción SVC SuperVisor Call es una excepción que nos permite pasar del modo no privilegiado a atender una excepción. Se puede utilizar para atender algún periférico como por ejemplo podría ser atender el UART.
# ISA
## 1. ¿Qué son los sufijos y para qué se los utiliza? Dé un ejemplo
## 2. ¿Para qué se utiliza el sufijo ‘s’? Dé un ejemplo
## 3. ¿Qué utilidad tiene la implementación de instrucciones de aritmética saturada? Dé un ejemplo con operaciones con datos de 8 bits.
## 4. Describa brevemente la interfaz entre assembler y C ¿Cómo se reciben los argumentos de las funciones? ¿Cómo se devuelve el resultado? ¿Qué registros deben guardarse en la pila antes de ser modificados?
## 5. ¿Qué es una instrucción SIMD? ¿En qué se aplican y que ventajas reporta su uso? Dé un ejemplo.
 
