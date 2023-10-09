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



 
